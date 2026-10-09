# Badges en steunpagina afmaken en klaarzetten voor Vercel

De vijf onderdelen staan al in de code: eigen badges, de badge-logica, de badge voor je eigen site, de steunpagina en de eigen betaalprovider. Wat nog ontbreekt: de database-updates, echte tests en het klaarzetten van de sleutels.

## Stap 1 - Sleutels opvragen (via een beveiligd formulier, nooit in de chat)
- **DATABASE_URL**: de app-verbinding met Neon (gebruiker `rout_app`).
- **MIGRATION_URL**: de eigenaar-verbinding met Neon, alleen nodig voor de database-updates.
- **PSP_ENCRYPTION_KEY**: wordt automatisch willekeurig aangemaakt voor de preview. Voor Vercel kies je zelf een waarde van minstens 32 tekens.
- **APP_SESSION_SECRET / BETTER_AUTH_SECRET, BETTER_AUTH_URL**: nodig om in te loggen.
- **SCALEWAY_ACCESS_KEY, SCALEWAY_SECRET_KEY, SCALEWAY_ENDPOINT, SCALEWAY_REGION, SCALEWAY_DEFAULT_BUCKET**: nodig om de foto's van de steunpagina en de badge-logo's te uploaden.
- **ALTCHA_HMAC_KEY**: wordt automatisch aangemaakt als die ontbreekt.

## Stap 2 - Database-updates
- De updates 57 (eigen badges) en 58 (steunpagina en versleutelde sleutels) uitvoeren, eerst als proefrun en daarna echt.
- Controleren dat de app-gebruiker de nieuwe tabellen kan lezen en schrijven.

## Stap 3 - Strengere regels volgens jouw instructies
- **Betaalproviders**: het paneel verschijnt alleen voor geverifieerde leden met een goedgekeurde Bedrijfsbadge. Dat wordt ook op de server gecontroleerd. De QR-code en de IBAN blijven altijd de basis.
- De verplichte disclaimer letterlijk tonen: "ROUT is geen betaalverwerker en neemt geen commissie..."
- Op de steunpagina staat de QR bovenaan. De betaalknoppen voor Kaart, Bancontact en Wero (alleen bij Mollie) staan eronder, en alleen als er een geldige sleutel is gekoppeld.
- Bij een Privacy-schild worden de wettelijke naam en het land nooit naar de publieke pagina gestuurd. Dat geldt ook voor de site-badge.
- De Influencer- en Bedrijfsbadge zijn pas te kiezen na goedkeuring.

## Stap 4 - Testen in de preview
- Als admin: een badge aanmaken, toekennen op @handle, de houders bekijken, intrekken, en het blok in het gebruikersbeheer controleren.
- Als geverifieerd lid: de steunpagina instellen met IBAN, bedragen en 3 bijgesneden foto's, en daarna `/naam/tip` openen. Controleren dat de QR meeverandert met het bedrag.
- Als gratis alias of niet-geverifieerd lid: het paneel is vergrendeld.
- De site-badge controleren op een lichte en een donkere achtergrond.
- De volledige controle van de code opnieuw uitvoeren en eventuele fouten oplossen.

## Stap 5 - Vercel-checklist
- ENVIRONMENT.md en .env.example bijwerken met alle nieuwe namen.
- Een korte lijst opleveren met welke waarden je in Vercel invult. Lovable kan sleutels niet zelf naar Vercel overzetten.
- Het te lange notitiebestand inkorten.

## Technisch
- Migraties via `bun scripts/migrate.ts` met MIGRATION_URL. Het script weigert te draaien als die gelijk is aan DATABASE_URL.
- De PSP-gate komt in `tip-page.server.ts`: geverifieerd, plus root handle, plus goedgekeurde business.

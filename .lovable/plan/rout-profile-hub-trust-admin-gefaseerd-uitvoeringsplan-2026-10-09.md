# ROUT Profile Hub, Trust & Admin — gefaseerd uitvoeringsplan

## Doel
De Profile Hub wordt een veilige draft-first editor met expliciet publiceren, geïntegreerde sociale verificatie, echte componentstatistieken, uitgebreide modulaire vormgeving en een bankwaardig trust-systeem. De bestaande Neon/Better Auth/Scaleway/Vercel-architectuur blijft leidend.

## Bevestigde uitgangssituatie
- De editor schrijft nu na korte debounce rechtstreeks naar het live profiel; undo/redo en opslagfeedback bestaan al, maar er is nog geen privéconcept.
- Referral staat nog in de Profile Hub; de header heeft geen Invite-knop en `/r/<handle>` wordt niet door de deel-UI gebruikt.
- Admin-zoeken, bulk suspend/ban/cleanse, VIP/handlebeheer en snelle gebruikersacties bestaan grotendeels al.
- Sociale verificatie bestaat apart van de componentenlijst. Alleen servermatig gemeten volgeraantallen worden gebruikt.
- Publieke profielen hebben een brede variant, maar uitlijning en enkele ontwerpinstellingen worden niet volledig toegepast.
- Er zijn 12 footerstijlen, 7 bezoekseffecten, 152 avatarkaders en 17 decoraties. De algemene `customDesign`-schakelaar blokkeert nu fijnmazige instellingen.
- Het volledige adres-/document-/periodieke herverificatiesysteem uit de aangeleverde richtlijn bestaat nog niet.
- De huidige transparante favicon is slechts 48×48 pixels; de bestaande transparante 192×192 variant biedt dezelfde basis voor een scherpere faviconset.

## Fase 1 — Betrouwbare kernflow en echte concepten
1. Voeg een aparte, eigenaar-gebonden conceptopslag toe voor alias- en geverifieerde profielen; bestaande live profieldata blijft de publieke bron.
2. Laat alle Studio-wijzigingen alleen het concept en de lokale preview bijwerken. Autosave bewaart het privéconcept, niet het live profiel.
3. Voeg vaste acties toe voor **Publiceren** en **Wijzigingen verwerpen**, met revisiecontrole zodat twee tabbladen geen wijzigingen stil overschrijven.
4. Publiceren valideert en kopieert het concept atomair naar live, ververst de publieke cache en toont `Publiceren…` / `Gepubliceerd ✓` / herstelbare foutstatus.
5. Behoud de bestaande geschiedenisstack en Ctrl/Cmd+Z, Ctrl/Cmd+Y en Shift+Ctrl/Cmd+Z; history werkt uitsluitend op het concept.
6. Audit en test alle servermatige opslagpaden voor geverifieerd profiel en privacy-alias, inclusief retries, navigatiewaarschuwing en herstel na een mislukte write.
7. Verwijder “Primaire kanalen” uit Basisinformatie; sociale gegevens worden alleen nog via Links & Inhoudscomponenten beheerd.
8. Behoud het huidige faviconontwerp en de transparante achtergrond, maar maak een scherpere faviconset op meerdere standaardformaten vanuit de beste bestaande bron, inclusief een hoge-resolutie 512×512 PNG; verander logo, kleur of uitsnede niet.

## Fase 2 — Invite, componenten, verificatie en statistieken
1. Verwijder ReferralPanel en ReferralAnalytics uit de Profile Hub.
2. Voeg voor ingelogde leden een **Invite**-actie in de gedeelde header en mobiele navigatie toe, met modal, native delen en kopiëren.
3. Gebruik exact:
   - geverifieerd: `https://rout.be/r/<handle>`
   - gratis alias: `https://rout.be/r/u/<alias>`
   - tekst: `Claim je soevereine digitale identiteit op ROUT via mijn uitnodiging: <url>`
4. Maak beide referralroutes geldig, behoud first-touch attributie, voorkom zelfverwijzingen en valideer de gever voordat attributie wordt geclaimd.
5. Integreer sociale verificatie in iedere relevante componentkaart: statusmarkering, inline controleren, hercontroleren en uitleg.
6. Open direct na toevoegen een verificatievenster met **Nu verifiëren** en **Overslaan**. Een later verwijderde ROUT-link wordt zichtbaar oranje/grijs en verliest de groene status.
7. Houd volgeraantallen uitsluitend server-geverifieerd; voeg geen handmatige teller toe.
8. Vervang geschatte componentklikken door echte component-events met privacyvriendelijke aggregatie. Toon eigen metrics binnen de componentkaart; publieke statistieken verschijnen alleen wanneer de bijbehorende profielinstelling/knop actief is.

## Fase 3 — Volledig trust-systeem en adminreview
1. Voeg aparte trusttabellen toe voor identiteit, e-mail, telefoon, adres, bewijsdocumenten, reviewbesluiten, correctievoorstellen, termijnen en audit-events. Rollen blijven uitsluitend in de bestaande aparte `user_roles`-structuur.
2. Statusmodel per eigenschap:
   - groen: officieel geverifieerd, met exacte verificatiedatum;
   - grijs/neutraal: door gebruiker toegevoegd, met toevoegdatum en uitleg;
   - verlopen/actie nodig: grace-periode of herverificatie overschreden.
3. Voeg veilige bewijs-van-adres-upload toe via private Scaleway-objecten onder de gebruikersnamespace; Neon bewaart alleen metadata. Downloadlinks voor reviewers zijn kortlevend en alleen servermatig uitgegeven.
4. Bouw in Studio de adresflow: upload, ingediend, in review, goedgekeurd, correctie voorgesteld, afgewezen, verlopen en wachttijd.
5. Bouw in admin een aparte trust-inbox met documentinspectie, goedkeuren, afwijzen en gecorrigeerd adres voorstellen. Iedere actie wordt geaudit en gemeld.
6. De gebruiker kan een correctievoorstel éénmaal accepteren of afwijzen. Afwijzen, negeren of opnieuw indienen volgt de vereiste zesmaandenblokkade.
7. Dwing adreswijzigingen servermatig af tot maximaal eenmaal per zes maanden; adresherverificatie wordt standaard na 30 maanden vereist, configureerbaar binnen 24–36 maanden.
8. Jaarlijkse e-mailherverificatie gebruikt een eenmalige, gehashte magic-linktoken. Jaarlijkse telefoonherverificatie gebruikt een gehashte, kortlevende SMS-code met rate limiting.
9. Voeg een beveiligde cronroute toe die komende/verlopen controles verwerkt, reminders verstuurt en na de grace-periode groene status terugzet naar verlopen.
10. Toon trustmarks met toegankelijke modal/tooltip op het publieke profiel, zonder privégegevens of documenten prijs te geven.
11. Breid `/admin/users` alleen aan waar nog gaten zijn: document/social-evidence inzicht en expliciete feature/content-toggles. Bestaande zoek-, bulk-, VIP-, verify-, bio-, avatar- en danger-zone-acties worden hergebruikt, niet dubbel gebouwd.

## Fase 4 — Publieke layout, vCard en modulaire vormgeving
1. Maak de publieke desktopinhoud maximaal `max-w-2xl`; links worden pas vanaf `lg` twee kolommen. Achtergrond en bezoek-FX blijven viewportbreed.
2. Laat avatar, kop en linkkolom werkelijk links/midden/rechts uitlijnen. Breid sociale iconen uit met floating links/rechts, inline en gridposities.
3. Verwijder de algemene Custom-mode lock. Achtergrond, knoppen, typografie, status en footer krijgen elk een eigen aan/uit-schakelaar en instellingenmodal.
4. Voeg semantisch opgeslagen controles toe voor hexkleuren, gradienthoek, randdikte, schaduw, blur, glow, letterafstand en tekstschaduw; waarden worden servermatig begrensd en genormaliseerd.
5. Maak **Interactie & Bezoek FX** een eigen onderdeel en breid de bibliotheek uit met cyberpunk, seizoenen, cinematografisch, sparks, confetti en matrixvarianten; alle effecten respecteren reduced motion en ruimen zichzelf op.
6. Bouw minimaal 50 procedurele footerstijlen in duidelijke categorieën, waaronder handgetekend, marquee, neon, water, glas, retro-shadow en cyberpunk, met snelheid en kleurstops.
7. Synchroniseer de vCard-knop met de globale knopstijl. Neem alle ingeschakelde velden op, gebruik een automatisch gelokaliseerd label en voeg de permanente ROUT-profiel-URL altijd toe aan zowel URL als Note.
8. Breid aanwezigheid uit met custom emoji op transparante achtergrond. Maak de statusregel optioneel als Discord-/stripbubble met kleur, rand, glow, tekst en staart.
9. Behoud de bestaande 152 avatarkaders en breid decoraties uit tot 100+ procedurele presets. Gebruik zoeken, categorie-pills, trending, favorieten en bestaande paginering/CSS-containment voor snelle rendering.

## Fase 5 — Productieharding en Vercel-oplevering
1. Voeg idempotente Neon-migraties toe vanaf het volgende vrije nummer en voer ze uitsluitend met de eigenaarverbinding uit; `MIGRATION_URL` komt niet in Vercel.
2. Test rechten, servervalidatie, uploads, signed URLs, concept/publicatieconflicten, trusttermijnen, adminrollen en publieke datalekken.
3. Voeg gerichte unit-, integratie- en route-smoketests toe en doorloop de hoofdflows als echt lid én admin.
4. Controleer mobiel en desktop visueel, toetsenbordbediening, reduced motion, lange teksten, foutstatussen en donkere/lichte modus.
5. Controleer favicontransparantie, scherpe randen en browser-/PWA-weergave op alle gegenereerde formaten.
6. Werk `ENVIRONMENT.md` en `.env.example` bij en lever één Vercel-checklist op met alleen noodzakelijke variabelen.

## Technische uitgangspunten
- Database: uitsluitend Neon; runtime blijft `rout_app`, migraties blijven eigenaar-only.
- Authenticatie: bestaande Better Auth-sessies; iedere gevoelige actie valideert servermatig gebruiker en rol.
- Opslag: bewijsdocumenten privé in Scaleway, nooit publiek en nooit als databaseblob.
- E-mail: uitsluitend de bestaande niet-blokkerende gelokaliseerde e-mailservice.
- Publieke pagina’s lezen alleen gepubliceerde data; concepten en documenten krijgen geen publieke leesroute.
- Nieuwe kleuren en stijlen worden semantische tokens/presets, geen losse hardcoded themawaarden in pagina’s.

## Benodigde secrets vóór de betreffende fase
- **Fase 3 e-mail:** bestaande `BREVO_API_KEY` en afzenderconfiguratie moeten in Vercel geldig zijn.
- **Fase 3 documenten:** bestaande `SCALEWAY_*` bucketgegevens moeten geldig zijn.
- **Fase 3 SMS:** een SMS-provider is nog niet bevestigd. Bij start van die stap wordt één provider gekozen en worden de benodigde Vercel-secrets veilig toegevoegd; secrets worden nooit in broncode of chat herhaald.
- Bestaande auth-, database- en encryptiesleutels blijven ongewijzigd; rotatie gebeurt alleen expliciet.

## Oplevermomenten
Elke fase eindigt in een apart testbaar, deploybaar punt. Na Fase 1 blijft de oude publieke ervaring functioneren, maar Studio-wijzigingen zijn voortaan veilig concept-first. Latere fasen bouwen daarop zonder tussentijds half-open trust- of documentroutes te publiceren.

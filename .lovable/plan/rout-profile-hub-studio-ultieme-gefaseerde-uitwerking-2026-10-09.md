# ROUT Profile Hub Studio — ultieme gefaseerde uitwerking

## Doel
De Profile Hub wordt een veilige concept-first editor met een hoogwaardige, gelaagde Design Studio: eerst sterke kant-en-klare stijlen, daarna vrije aanpassing per onderdeel en ten slotte een diep instellingenvenster. Publieke profielen blijven snel, toegankelijk en visueel identiek aan de preview. De bestaande Neon-, Better Auth-, Scaleway- en Vercel-architectuur blijft behouden.

## Bevestigde uitgangssituatie
- Studio slaat wijzigingen nu automatisch rechtstreeks op het openbare profiel op; er is nog geen privéconcept of expliciete publicatie.
- De algemene `customDesign`-schakelaar blokkeert achtergrond-, knop- en typografie-instellingen; sommige opgeslagen instellingen hebben nog geen bediening of zichtbare werking.
- Er zijn 152 avatarkaders, maar vooral door kleurvarianten van acht vormen. Avatardecoraties tellen slechts 16 echte ontwerpen en bezoekseffecten slechts zeven actieve varianten.
- De gedeelde zoek-/favorieten-/categorie-interface voor kaders en decoraties is al een goede schaalbare basis.
- Sociale verificatie staat nog los van componentkaarten en componentklikken zijn nog niet werkelijk gemeten.
- Het volledige trust-, document- en periodieke herverificatiesysteem ontbreekt nog.

## Fase 1 — Veilige concepten en publiceren
1. Voeg eigenaar-gebonden conceptopslag toe voor geverifieerde profielen en privacy-aliassen, met revisienummer en tijdstempel.
2. Laat autosave uitsluitend het privéconcept bewaren. De lokale preview volgt het concept direct; publieke pagina’s lezen alleen gepubliceerde data.
3. Voeg vaste acties toe voor **Publiceren** en **Wijzigingen verwerpen**, met duidelijke statussen, herstelbare fouten en bescherming tegen conflicten tussen meerdere tabbladen.
4. Publiceren valideert en kopieert het concept atomair naar live; verwerpen herstelt het concept naar de laatst gepubliceerde versie.
5. Behoud undo/redo, toetsencombinaties, navigatiewaarschuwing en retries, maar laat geschiedenis uitsluitend op het concept werken.
6. Genereer vanuit het bestaande transparante merkbeeld een scherpe faviconset, inclusief 512×512, zonder logo, kleur of uitsnede te veranderen.

## Fase 2 — Gelaagde Design Studio
1. Verwijder de globale Custom-lock. Achtergrond, knoppen, typografie/naam, avatar/header, status, footer en interactie krijgen elk een eigen **Aanpassen**-schakelaar.
2. Iedere ontwerpsectie krijgt drie niveaus:
   - **Kiezen:** visuele, kant-en-klare presets met live voorbeeld.
   - **Aanpassen:** de actieve preset valt uiteen in afzonderlijke eigenschappen die direct bewerkbaar zijn.
   - **Geavanceerd:** een volledig instellingenvenster met sliders, exacte waarden, hexvelden, uploads en reset per eigenschap.
3. Een preset blijft de bron voor startwaarden; inschakelen van Aanpassen kopieert de zichtbare presetwaarden zodat niets onverwacht verspringt.
4. Voeg opgeslagen, servermatig begrensde instellingen toe voor gradienthoek en kleurstops, lichtpositie/-sterkte, textuur, beweging, blur, overlay, randdikte, schaduw, glow, letterafstand, regelafstand, titelgrootte, tekstschaduw en animatie-intensiteit/snelheid.
5. Activeer en render de bestaande dode instellingen voor titelgrootte, knopgrootte/-effect, bannerhoogte, avatargrootte/-uitlijning/-overlap; voeg regressietests voor normalisatie en zichtbare stijlberekening toe.
6. Maak bediening compact en professioneel: visuele tegels voor presets, schakelaars voor onderdelen, sliders voor numerieke waarden, kleurvelden met volledig kleurvenster en een zijpaneel/drawer voor diepe instellingen.
7. Gebruik dezelfde `ProfileView` voor publieke pagina en preview, zodat beide uitvoeringen exact gelijk blijven.

## Fase 3 — Avatar-, decoratie- en effectenbibliotheek
1. Behoud alle 152 bestaande kaders, maar onderscheid de beste ontwerpen duidelijk en voeg handgemaakte gelaagde kaders toe met textuur, overlay en subtiele animatie in plaats van alleen herkleuring.
2. Breid avatardecoraties uit tot minimaal 100 werkelijk bruikbare presets via een combinatie van zorgvuldig ontworpen basiselementen, kleur-/materiaalvarianten en samengestelde sets. Voeg categorieën toe zoals minimal, professioneel, gaming, kawaii, natuur, feest, seizoen, cyber en elite.
3. Maak decoraties aanpasbaar: primaire/secundaire kleur, materiaal, positie, schaal, rotatie, gloed, beweging, snelheid en intensiteit, met veilige grenzen.
4. Voeg samengestelde stijlen toe die kader, decoratie, status en bezoekseffect combineren, zonder gebruikers te verhinderen onderdelen afzonderlijk te wijzigen.
5. Breid bezoekseffecten uit met subtiel, professioneel, sparks, meerdere confetti-/matrixvarianten, cyberpunk, seizoenen en cinematografische effecten. Voeg intensiteit, duur en afspeelfrequentie toe.
6. Respecteer `prefers-reduced-motion`, bied een stille/statische variant en ruim alle tijdelijke elementen/timers altijd op.
7. Behoud zoeken, categorieën, trending, favorieten, paginering en snelle rendering. Toon in miniaturen het echte resultaat met de huidige avatar.
8. Herstel de verouderde kadertest (24 versus 152) en voeg tests toe voor decoratienormalisatie, combinaties, effectopruiming en verminderde beweging.

## Fase 4 — Publiek profiel, componenten en analytics
1. Maak desktopinhoud maximaal `max-w-2xl`; schakel links pas vanaf groot desktopformaat naar twee kolommen. Achtergrond en bezoekseffecten blijven viewportbreed.
2. Laat avatar, kop, status, socials en linkkolom werkelijk links, midden of rechts uitlijnen. Voeg floating links/rechts, inline en gridposities voor socials toe.
3. Synchroniseer de vCard-knop met de globale knopstijl, lokaliseer het label en voeg de permanente ROUT-profiel-URL altijd aan URL en notitie toe.
4. Breid aanwezigheid uit met transparante custom emoji en een optionele Discord-/stripbubble met eigen tekst, kleur, rand, gloed en staart.
5. Bouw minimaal 50 procedurele footerstijlen in duidelijke categorieën, met aanpasbare kleuren en beweging waar passend.
6. Integreer sociale verificatie in elke relevante componentkaart: status, controleren, hercontroleren, overslaan en zichtbare degradatie wanneer bewijs later verdwijnt.
7. Registreer echte privacyvriendelijke component-events en toon eigen kliks per component en geaggregeerd in Analytics. Volgeraantallen blijven uitsluitend server-geverifieerd.

## Fase 5 — Trust, documenten en soevereine telefoonverificatie
1. Voeg aparte trusttabellen toe voor identiteit, e-mail, telefoon, adres, bewijsstukken, reviewbesluiten, correcties, termijnen en audit-events. Rollen blijven uitsluitend in de bestaande rollenstructuur.
2. Bouw private adresbewijsupload via Scaleway, een volledige gebruikersflow en een admin-inbox met kortlevende downloadlinks, correctievoorstellen en audittrail.
3. Dwing adreswijziging maximaal eenmaal per zes maanden en herverificatie standaard na 30 maanden af; jaarlijkse e-mailcontrole gebruikt een gehashte eenmalige magic link.
4. Bouw een provider-onafhankelijke telefoniegateway met één intern verzendcontract en verwisselbare kanaaladapters:
   - eigen Android SMS Gateway via beveiligde uitgaande API en ondertekende status-webhook;
   - SMS als primaire servergestuurde route;
   - RCS/iMessage alleen wanneer de eigen gateway aantoonbaar ondersteuning en afleverstatus biedt;
   - WhatsApp en Telegram via een verificatie-intent/bot-flow waarbij een servergegenereerde code aan een gekoppelde sessie wordt bevestigd.
5. Sla geen leesbare telefoonnummers of codes op: bewaar alleen een keyed hash voor nummermatching, een aparte versleutelde bezorgwaarde uitsluitend zolang verzending/herverificatie dit vereist, gehashte kortlevende codes, kanaal, pogingentellers en auditmetadata. Verwijder tijdelijke bezorgwaarden na bevestiging of verval.
6. Voeg strenge server-side limieten toe per account, telefoonhash, IP-risicosignaal en tijdvenster; codes zijn single-use, verlopen snel en antwoorden lekken niet of een nummer bestaat.
7. Weiger onbetrouwbare kanaalclaims: een chat-link zonder servermatig bewijs telt niet als verificatie. Kanaalstatussen zijn `verzonden`, `afgeleverd` waar ondersteund, `bevestigd`, `verlopen` of `mislukt`.
8. Voeg een beveiligde cronroute toe voor termijnen, herinneringen, grace-periodes en statusverval.

## Fase 6 — Productieharding en oplevering
1. Lever iedere fase als afzonderlijk testbaar punt op; er wordt geen half-open trust- of webhookroute gepubliceerd.
2. Voeg idempotente Neon-migraties toe vanaf het volgende vrije nummer, gespiegeld in beide bestaande migratielocaties, en pas ze alleen via de owner-verbinding toe.
3. Test rechten, revisieconflicten, publieke datalekken, uploads, signed links, gateway-webhooks, rate limiting, codehergebruik, adminrollen en alle normalisatiegrenzen.
4. Controleer Studio en publieke profielen visueel op mobiel en desktop, licht/donker, lange tekst, toetsenbord, reduced motion en trage apparaten.
5. Werk `ENVIRONMENT.md`, `.env.example`, `AGENTS.md` en de Vercel-checklist bij. Externe gatewaywaarden komen uitsluitend in veilige secrets, nooit in broncode.

## Technische details
- Neon blijft de enige database; runtime gebruikt de bestaande least-privilege verbinding en server-side autorisatie.
- Concepten krijgen een unieke sleutel per gebruiker en profielruimte plus optimistic concurrency via revisies.
- Nieuwe ontwerpwaarden blijven in genormaliseerde `display_prefs`; eigendom/rechten, truststatussen, events en verificatiepogingen krijgen eigen tabellen.
- De Android-gateway krijgt minimaal een basis-URL, gedeelde webhookondertekening, uitgaand authenticatiemiddel en strikte allowlist/replaybescherming. De concrete gatewayvelden worden pas gekoppeld wanneer de gekozen Android-server haar API-contract bekendmaakt.
- iMessage/RCS worden niet als gegarandeerde kanalen gepresenteerd zonder aantoonbare ondersteuning door de gateway en servermatig verifieerbare levering/bevestiging.

## Acceptatiecriteria
- Een Studio-wijziging wordt nooit publiek vóór **Publiceren**.
- Iedere ontwerpsectie werkt zelfstandig van preset tot exact geavanceerd niveau en blijft identiek in preview en publiek profiel.
- Minimaal 100 decoraties zijn doorzoekbaar, performant en visueel controleerbaar; 152 bestaande kaders blijven beschikbaar.
- Alle actieve effecten zijn opruimbaar, begrensd en reduced-motion-veilig.
- Publieke analytics gebruiken echte events; trustdetails, concepten, documenten, telefoonnummers en tokens lekken nooit via publieke routes.
- Telefoonverificatie accepteert alleen servermatig bevestigd bewijs en is bestand tegen replay, brute force en kanaalomleiding.

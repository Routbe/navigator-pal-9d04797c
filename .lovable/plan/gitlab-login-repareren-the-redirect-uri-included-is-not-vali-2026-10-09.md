# GitLab-login repareren ("The redirect URI included is not valid")

## Wat er nu misgaat
De terugkeer-link die we naar GitLab sturen, wordt elke keer opnieuw samengesteld uit het adres waarop de bezoeker binnenkomt. Dat gebeurt alleen niet als BETTER_AUTH_URL op Vercel is ingesteld. Komt iemand binnen via `www.rout.be`, het korte domein of een preview-adres van Vercel, dan sturen we een andere link mee dan `https://rout.be/api/auth/callback/gitlab`. GitLab weigert dan. Daarnaast vragen we alleen de toestemming `read_user`, terwijl je Group Application ook `openid`, `profile` en `email` verwacht.

De proxy van Vercel (`x-forwarded-proto`) is niet de boosdoener. De code zet een publiek adres al altijd op https.

## Wat ik ga aanpassen
1. **Vaste terugkeer-link voor GitLab.** We sturen altijd precies `https://rout.be/api/auth/callback/gitlab` mee: met https, zonder schuine streep op het einde en ongeacht het adres van de bezoeker. Die link gebruiken we zowel bij het inloggen als bij het ophalen van de toegangssleutel. Wil je toch een andere link gebruiken, dan kan dat via de instelling `GITLAB_REDIRECT_URI`.
2. **Juiste toestemmingen.** We vragen `openid`, `profile`, `email` en `read_user`, elk maar één keer.
3. **Adres van de GitLab-server opschonen.** Een schuine streep op het einde van `GITLAB_ISSUER` wordt verwijderd. Laat je het leeg, dan gebruiken we standaard `https://gitlab.com`.
4. **Geen controlefout meer bij andere adressen.** Begint iemand de GitLab-login op `www.rout.be` of op het korte domein, dan sturen we die eerst door naar `https://rout.be`. Alleen zo blijft de controlecookie geldig wanneer GitLab terugstuurt naar rout.be.
5. **Duidelijke melding in de logboeken.** Bij elke GitLab-login staat in de server-logboeken welke terugkeer-link is meegestuurd, zonder geheime gegevens. Zo zie je op Vercel meteen of die klopt.
6. ENVIRONMENT.md en .env.example bijwerken met `GITLAB_REDIRECT_URI` en `GITLAB_ISSUER`.

## Wat jij in GitLab controleert (Group → Settings → Applications)
- Redirect URI: precies `https://rout.be/api/auth/callback/gitlab`. Eén regel, zonder spaties of schuine streep op het einde.
- "Confidential" staat aan.
- De vinkjes `openid`, `profile`, `email` en `read_user` staan aan.
- Op Vercel: `BETTER_AUTH_URL=https://rout.be`, plus `GITLAB_CLIENT_ID` en `GITLAB_CLIENT_SECRET` uit deze Group Application.

## Technisch
- In `better-auth.server.ts` krijgt de GitLab-provider `redirectURI` (van `canonicalAppUrl()` of `GITLAB_REDIRECT_URI`) en `scope: ["openid","profile","email"]`. `read_user` voegt de bibliotheek al standaard toe. Better Auth gebruikt `options.redirectURI` zowel voor de authorize-URL als voor de token-uitwisseling.
- Een guard in `api_/auth/$.ts`: bij `sign-in/social` met provider gitlab, op een host die niet de canonieke is, volgt een 307 naar de canonieke host.

# Klimatdata – publik webb

Den här repositorien ska endast innehålla den **krypterade HTML-dashboarden** och eventuell dokumentation utan hemligheter.

Webbadress efter att GitHub Pages aktiverats: https://lulea-statistik.github.io/klimat-data-webb/

## Säkerhet och drift
- Källkod och databeräkning hanteras i det **privata** repot `Lulea-statistik/klimat-data`.
- Inga lösenord, privata data, API-token, okrypterade HTML-kopior eller individuella CSV-exporter får läggas i det här publika repot.
- Krypterad dashboard byggs med AES-256-GCM och PBKDF2/SHA-256 (600000 iterationer), och publiceras från det privata repots GitHub Actions.
- Kryptering ger ett delat lösenord utan användarhantering och är **inte** samma sak som serverstyrd åtkomstkontroll. Den krypterade filen är offentligt nedladdningsbar.
- Enbart den ursprungliga HTML-filen krypteras. Lägg därför **inte** till okrypterade externa datafiler, AJAX-anrop till privata resurser eller fristående känsliga JS-filer i dashboarden.
- Historiska Git-commits är också publika. Råfiler och hemligheter får aldrig publiceras, inte ens tillfälligt.
- För att byta lösenord: ändra GitHub Actions-hemligheten `CLIMATE_DASHBOARD_PASSWORD` och kör publiceringsarbetsflödet igen.

## Aktivering
1. I publika repot: Settings > Pages > Deploy from a branch; välj `main`, `/(root)` och Save.
2. I privata repot: Settings > Secrets and variables > Actions; lägg till `CLIMATE_DASHBOARD_PASSWORD` (minst 16 tecken, gärna slumpmässigt genererat).
3. Där: lägg till `CLIMATE_WEB_PUBLISH_TOKEN`, en **fine-grained** GitHub Personal Access Token med `Contents: Read and write` enbart för detta publika repo. Ge ingen annan åtkomst.
4. Kör workflow `Kryptera och publicera klimatdashboard` i det privata repot.
5. Verifiera att GitHub Pages visar lösenordsformuläret, att fel lösenord nekas och att rätt lösenord öppnar dashboarden.

**OBS:** Detta offentliga repo innehåller före konfiguration bara en platshållarsida, inte skyddad statistik.

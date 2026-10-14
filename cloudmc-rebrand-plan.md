# CloudMC Rebrandplan

## Doelen

- Zichtbare productnaam uniform maken:
  - plugin: `CloudMC`
  - portal: `CloudMC Portal`
- Nieuwe brandingassets toevoegen zonder gebruik van OpenMinetopia-merkassets.
- Bestaande functionaliteit behouden.
- Compatibiliteit behouden voor commands, permissions, data en integraties waar dat nodig is.
- Juridische herkomst en GPL-vermeldingen behouden.

## Fase 1: Veilige rebranding

- Pluginmetadata wijzigen:
  - projectnaam
  - artifactnaam
  - `paper-plugin.yml`
  - README
  - CI-artifactnamen
- Zichtbare pluginteksten wijzigen:
  - versie-info
  - helpteksten
  - logische defaults in configuratie
- Portal zichtbaar rebranden:
  - `APP_NAME` defaults
  - titels, foutpagina's, installerteksten en documentatie
  - compose/projectnamen, scripts en image-variabelen waar veilig
  - branding UI en standaard logo/favicons
- Nieuwe CloudMC-kleurset toevoegen:
  - koel blauw/cyaan met donkere neutralen
  - goede contrasten voor licht en donker thema

## Fase 2: Compatibele interne opschoning

- Nieuwe CloudMC-identifiers toevoegen zonder breuk:
  - extra plugin commandalias `cloudmc`
  - portal check/probe-strings naar CloudMC-termen
  - interne CSS prefix van `omt-*` naar `cloudmc-*` waar dit alleen frontend-intern is
- Configuratievoorbeelden generiek maken:
  - geen verzonnen domeinen
  - placeholders of `example.invalid`
  - expliciete opmerkingen waar gebruiker eigen waarden moet invullen

## Fase 3: Validatie

- Plugin:
  - `./gradlew test build`
  - metadata en JAR-naam controleren
  - resterende oude merkverwijzingen opnieuw scannen
- Portal:
  - `composer install`
  - `npm ci`
  - tests en productiebuild draaien
  - assetverwijzingen en layouts controleren
- Daarna resterende hits rubriceren:
  - licentie/herkomst
  - backward compatibility
  - externe dependency
  - onbedoelde oude branding

## Bewuste uitzonderingen

- Java rootpackage `nl.openminetopia` migreer ik niet blind in deze omgeving.
- Permissions met prefix `openminetopia.*` blijven voorlopig bestaan voor backward compatibility.
- Externe plugin-identifiers van derde partijen wijzig ik niet.
- Productie-domeinen, e-mailadressen en credentials worden niet verzonnen.

## Concreet eerste wijzigingspakket

- Plugin:
  - `settings.gradle`
  - `build.gradle.kts`
  - `src/main/resources/paper-plugin.yml`
  - `src/main/resources/default/messages.yml`
  - `src/main/java/.../OpenMinetopiaCommand.java`
  - `src/main/java/.../DefaultConfiguration.java`
  - `README.md`
  - `.github/workflows/gradle.yml`
- Portal:
  - `.env.example`
  - `README.md`
  - `CONTRIBUTING.md`
  - `SECURITY.md`
  - `docker-compose.yml`
  - `install.sh`
  - `pterodactyl/egg-openminetopia-portal.json`
  - `app/Console/Commands/*`
  - `app/Services/*`
  - `app/Models/BrandingSetting.php`
  - `resources/views/**/*`
  - `resources/css/app.css`
  - `tailwind.config.js`
  - `public/images/brand/*`
  - favicon-bestanden

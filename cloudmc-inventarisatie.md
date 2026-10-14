# CloudMC Inventarisatie

## Scope

- Bronrepository plugin: `https://github.com/OpenMinetopia/openminetopia`
- Bronrepository portal: `https://github.com/OpenMinetopia/portal`
- Lokale werkpaden: `/workspace/openminetopia` en `/workspace/portal`
- Werkbranches:
  - plugin: `feature/cloudmc-rebrand`
  - portal: `feature/cloudmc-rebrand`
- Back-upbranches:
  - plugin: `backup/pre-cloudmc-2026-10-14`
  - portal: `backup/pre-cloudmc-2026-10-14`

## Gitstatus

### Plugin

- Huidige branch: `master`
- Remote: `origin -> https://github.com/OpenMinetopia/openminetopia.git`
- Belangrijke remote branches:
  - `origin/master`
  - `origin/bugfix/banking-loading`
  - `origin/feature/pin-consoles`
  - `origin/feature/vehicles`
- Lokale status bij start: schoon, `master...origin/master`

### Portal

- Huidige branch: `main`
- Remote: `origin -> https://github.com/OpenMinetopia/portal.git`
- Belangrijke remote branches:
  - `origin/main`
  - `origin/dev`
  - `origin/design-v2`
- Lokale status bij start: schoon, `main...origin/main`

## Licenties

- Beide repositories gebruiken GPL-3.0.
- Vereiste herkomst- en auteursvermeldingen moeten behouden blijven.
- Een rebranding mag de oorsprong van de code niet verhullen.

## Technische inventarisatie

### Plugin

- Taal: Java
- Platform: Paper
- Buildtool: Gradle Kotlin DSL
- Wrapper: Gradle `9.5.0`
- Projectnaam: `OpenMinetopia`
- Group: `nl.openminetopia`
- Java target: `25`
- Runtimekoppelingen:
  - PlaceholderAPI
  - Vault
  - WorldEdit
  - WorldGuard
  - Skript
  - Citizens
  - FancyNpcs
  - LabyMod
  - QualityArmory
- Belangrijke kenmerken:
  - Single-module plugin
  - Veel YAML-defaults in `src/main/resources/default`
  - REST API via Vert.x
  - Portalintegratie via `portal.url` en tokens

### Portal

- Talen: PHP, Blade, JavaScript, CSS
- Frameworks: Laravel 11, Vite, Tailwind, Alpine.js
- Buildtools: Composer, npm, Vite
- Runtime:
  - PHP `^8.2` in Composer
  - Dockerimage op PHP 8.4 / FrankenPHP
  - Node 22 in Docker/builddocs
- Architectuur:
  - Single-mode en hosted multi-tenant mode
  - Portal praat met plugin via HTTP API
  - Branding instelbaar via database en adminscherm

## Hoofdstructuur

### Plugin

- `src/main/java/nl/openminetopia`
- `src/main/resources`
- `.github/workflows`
- `build.gradle.kts`
- `settings.gradle`

### Portal

- `app`
- `config`
- `database`
- `resources`
- `public`
- `routes`
- `tests`
- `docker`
- `pterodactyl`

## Brandingverwijzingen

### Plugin

- Zichtbare productnaam `OpenMinetopia`:
  - `README.md`
  - `src/main/resources/paper-plugin.yml`
  - `src/main/resources/default/messages.yml`
  - `.github/workflows/gradle.yml`
- Java package namespace:
  - `nl.openminetopia`
- Interne identifiers:
  - groupId `nl.openminetopia`
  - shaded relocate-paden `nl.openminetopia.shaded.*`
  - PlaceholderAPI expansion class `OpenMinetopiaExpansion`
- Legacy/default configuratie:
  - database default `openminetopia`
  - portal default `portal.openminetopia.nl`
- Backward-compatible commandaliases:
  - `openminetopia`
  - `minetopia`
  - `omt`
  - `sdb`

### Portal

- Zichtbare productnaam `OpenMinetopia Portal`:
  - `README.md`
  - `SECURITY.md`
  - `CONTRIBUTING.md`
  - foutpagina's en authviews
  - installerteksten
  - Pterodactyl egg
- Oude domeinen/hosts:
  - `openminetopia.nl`
  - `wiki.openminetopia.nl`
  - `*.mtportal.nl`
  - `central.mtportal.nl`
- Oude container/image identifiers:
  - `ghcr.io/openminetopia/portal`
  - `ghcr.io/openminetopia/portal-pterodactyl`
  - compose projectnaam `openminetopia-portal`
- Demo/adressen:
  - `demo@openminetopia.nl`
  - `*@demo.openminetopia.nl`
- CSS/interne prefix:
  - `omt-*`

## Compatibiliteitscontracten

Deze verwijzingen mogen niet blind worden hernoemd:

- Java rootpackage `nl.openminetopia`
  - raakt imports, package-declaraties, reflection, public API en shaded relocations
  - vereist Java-aware refactoring
- Permissions zoals `openminetopia.reload`
  - kunnen door serverscripts en permissieplugins gebruikt worden
- Bestaande commandaliases
  - kunnen in documentatie en automatisering gebruikt worden
- REST API-paden
  - moeten met portal samen gecontroleerd worden
- Database schema's en bestaande opslag
  - niet hernoemen zonder migratieplan
- Hosted platform verwijzingen
  - alleen vervangen door configureerbare placeholders, niet door verzonnen productiegegevens

## Belangrijkste risico's

- Plugin target `Java 25` is zwaar en mogelijk onpraktisch voor gangbare hostingomgevingen.
- Plugin build/runtime dependency-versies wijken op een paar plaatsen van elkaar af.
- Volledige package-migratie naar `nl.cloudmc` is in deze omgeving niet veilig te automatiseren zonder een echte Java-aware refactoringtool.
- Portal kent single en hosted mode; documentatie en defaults moeten beide scenario's blijven ondersteunen.
- Publieke domeinen, e-mailadressen en container registry-paden mogen niet verzonnen worden; ze moeten configureerbaar of expliciet als placeholder worden gedocumenteerd.

## Uitvoeringsstrategie

- Eerst zichtbare branding, metadata, configureerbare defaults en assets vervangen.
- Daarna veilige interne identifiers aanpassen waar dat geen compatibiliteitscontract breekt.
- Oude namen die extern contractueel zijn behouden:
  - licentie/herkomst
  - backward compatibility
  - externe afhankelijkheden
- Na wijzigingen opnieuw zoeken op oude branding en per hit classificeren.

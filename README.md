# repro-quarkus-i37649

To reproduce issue run `./gradlew clean build` followed by `docker compose up -d`. Expected: tables are created in `foo`
schema as schema is overridden in [config](config/application.yaml); actual: tables are created in `public` schema

now run `docker compose down`, go to [config](config/application.yaml), comment first property and uncomment second.
Relaunch service with `docker compose up -d`, ensure that tables are created in `foo` schema

now run `docker compose down` and change Quarkus version in [properties file](gradle.properties) to 3.5.1. Rebuild
container with `./gradlew clean build` and relaunch service with `docker compose up -d`, ensure that tables are created
in `foo` schema and it doesn't matter which property is specified in [config](config/application.yaml) (try both)

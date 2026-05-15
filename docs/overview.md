# Repository Overview

`openmrs-core` is a multi-module Maven project. The top-level layout, as
described in the project README, is:

| Path | Purpose |
| --- | --- |
| `api/` | Java and resource files for building the Java API JAR file. |
| `tools/` | Meta code used during compiling and testing (e.g. doclets). Not shipped in any released binary. |
| `web/` | Java and resource files that are used in the webapp/WAR file. |
| `webapp/` | Files used in building the WAR file (contains JSP files on older versions). |
| `test/` | Shared test code and fixtures consumed by other modules. |
| `test-suite/` | Cross-module integration test suite. |
| `bom/` | Bill-of-materials POM that pins dependency versions for the platform. |
| `liquibase/` | Liquibase changelogs and helpers for database schema management. |
| `pom.xml` | The main Maven file used to build and package OpenMRS. |

## Supporting Files at the Root

- `Dockerfile`, `docker-compose.yml`, `docker-compose.override.yml`,
  `docker-compose.es.yml`, `docker-compose.grafana.yml` — container build and
  orchestration for development, Elasticsearch and Grafana profiles.
- `startup.sh`, `startup-dev.sh`, `startup-init.sh`, `wait-for-it.sh` — entry
  point and bootstrap scripts used by the container images.
- `mvnw`, `mvnw.cmd`, `.mvn/` — the Maven Wrapper, so contributors do not need
  a system-wide Maven install.
- `checkstyle.xml`, `ruleset.xml`, `spotbugs-exclude.xml` — static analysis and
  code-style configuration.
- `bamboo-specs/` — Bamboo CI pipeline definitions.

## Build Output

A full build produces `webapp/target/openmrs.war`, which is the deployable
artifact for Tomcat, Jetty or the provided Docker images.

## Extending OpenMRS

OpenMRS has a modular architecture: most features beyond the platform are
shipped as separate modules. Before writing a new module, check the
[OpenMRS Module Repository](https://addons.openmrs.org/) for an existing one.

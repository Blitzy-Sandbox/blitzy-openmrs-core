# Build and Setup

This page summarises the build workflows documented in the repository README.

## Prerequisites

- **Java JDK** — OpenMRS is a Java application. Building the `master` branch
  requires a JDK of minimum version 8.
- **Maven** — Install [Maven](https://maven.apache.org/). Verify that Maven is
  using the correct JDK with `mvn -version`. The repository also ships the
  Maven Wrapper (`./mvnw`), which is the recommended invocation.
- **Git** — Install [git](https://git-scm.com/) and clone the repository.

## Local Maven Build

From the repository root:

```bash
./mvnw clean package
```

This generates `webapp/target/openmrs.war`, which can be deployed into a
servlet container such as Tomcat or Jetty.

## Run with Jetty (Development)

```bash
cd webapp
../mvnw jetty:run
```

To run Jetty on a custom port:

```bash
mvn -Djetty.http.port=8081 jetty:run
```

Once started, the application is available at `http://localhost:8080/openmrs`.

## Docker Build

Development image:

```bash
docker compose build
docker compose up
```

Production image (Tomcat + `openmrs.war`):

```bash
docker compose -f docker-compose.yml build
docker compose -f docker-compose.yml up
```

The development image exposes port `8000` for remote debugging.

### Pre-built Images

CI publishes images to <https://hub.docker.com/r/openmrs/openmrs-core>:

```bash
TAG=nightly docker compose -f docker-compose.yml up
TAG=dev     docker compose up
```

## Optional Profiles

### Elasticsearch Backend

```bash
docker compose -f docker-compose.yml -f docker-compose.override.yml -f docker-compose.es.yml up
```

After switching backends, rebuild the search index from
**Legacy UI -> Administration -> Search Index**, or via the `searchindexupdate`
REST endpoint.

### Grafana Monitoring

```bash
docker compose -f docker-compose.yml -f docker-compose.override.yml -f docker-compose.grafana.yml up
```

Grafana is available at <http://localhost:3000>.

## Further Reading

- [Getting Started as a Developer](https://openmrs.atlassian.net/wiki/spaces/docs/pages/25477022/Getting+Started+as+a+Developer)
- [Maven on OpenMRS Wiki](https://wiki.openmrs.org/display/docs/Maven)
- `CONTRIBUTING.md` in the repository root

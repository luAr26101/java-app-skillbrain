# SkillBrain Java App

Acesta este proiectul de bază pentru Modulul 4, folosit progresiv în toate exercițiile de CI/CD.

## Stack

- Java 17
- Spring Boot 3
- Maven
- JUnit 5

## Endpoints

- `GET /` -> UI web pentru demo
- `GET /api/health` -> status aplicație
- `GET /api/info` -> mesaj de status al aplicației
- `GET /api/pipeline` -> pașii pipeline-ului folosiți în laborator

## Rulezi local

```bash
mvn clean test
mvn spring-boot:run
```

Aplicația pornește implicit pe `http://localhost:8080`, iar pagina principală este UI-ul web.

## Milestones pentru laborator

1. **CI de bază**: build + test în GitHub Actions.
2. **Publish artefact**: JAR upload ca artifact în workflow.
3. **Containerizare**: build/push imagine în GHCR.
4. **Deploy**: deploy în mediu cloud (ex. Elastic Beanstalk).
5. **Backup**: arhivare + upload în S3 pe schedule.

## Ce trebuie să faci tu

Repo-ul nu include workflow-urile finale de curs. Le adaugi tu pas cu pas în `.github/workflows`, conform lecțiilor.

## CI/CD Artifacts & Docker Images

### Maven Package (Github Packages)

- **Tag folosit:** `0.0.1-SNAPSHOT`
- **Motiv:** Maven foloseste versiunea din `pom.xml`. Pentru fiecare commit, workflow-ul `publish-artifact.yml` publică același artifact cu această versiune în GitHub Packages.

### Docker Images (GHCR)

- **Tag folosit:** `sha<commit>`
  - Fiecare build are tag unic asociat SHA-ul commit-ului
  - Avantaj: poti identifica exact codul sursa pentru imaginea respectiva
- **Tag folosit:** `latest`
  - Reprezinta ultima versiune stabila/deployata
  - Avantaj: simplifica testarea si rularea rapida a imaginii fara a verifica SHA

**Exemple concrete:**

```text
ghcr.io/skillbrain-devops/java-app:sha-abc123def
ghcr.io/skillbrain-devops/java-app:latest
```

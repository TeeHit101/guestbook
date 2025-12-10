Gästbok-applikation

 CI/CD-pipeline (GitHub Actions)

Detta projekt använder GitHub Actions för att automatisera bygg- och distributionsprocessen. Arbetsflödet definieras i `.github/workflows/deploy.yml` och består av följande tydliga steg:

1. Bygg och pusha images

- Checka ut kod: Arbetsflödet börjar med att ladda ner den senaste koden från repot.
- Logga in i registret: Loggar in säkert i GitHub Container Registry (ghcr.io).
- Bygg Backend: Backend-koden (i mappen `/backend`) byggs till en Docker-image och pushas till `ghcr.io/teehit101/guestbook-backend:latest`.
- Bygg Frontend: Frontend-koden (i mappen `/frontend`) byggs till en Docker-image och pushas till `ghcr.io/teehit101/guestbook-frontend:latest`.

2. Distribuera till OpenShift

- Installera verktyg: Installerar OpenShift CLI-verktyget (`oc`).
- Autentisera: Loggar in i OpenShift-klustret med hjälp av hemligheterna `OPENSHIFT_SERVER` och `OPENSHIFT_TOKEN`.
- Tillämpa konfigurationer:
  - Kör `oc apply -f openshif-yaml/` för att uppdatera alla Kubernetes/OpenShift-resurser (Deployments, Services, etc.) som definieras i den mappen.
- Starta om distributioner (Deployments):
  - Kör `oc rollout restart` för både backend- och frontend-distributionerna. Detta säkerställer att poddarna startar om och hämtar de nya Docker-images som vi precis byggde.

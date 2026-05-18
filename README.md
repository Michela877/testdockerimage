
## Prerequisiti

- Kubernetes cluster con Argo CD installato
- Harbor registry accessibile dal cluster
- Repository GitHub con permessi di scrittura
- `kubectl` configurato per accedere al cluster

## Installazione

### 1. Crea i Secret per le credenziali

```bash
# Secret per Harbor (usa il robot account) creare sul progetto harbor e selezionare robot
kubectl create secret generic harbor-creds -n argocd \
  --from-literal=username='robot$michela877+argocd-image-updater' \
  --from-literal=password='IL_TUO_PASSWORD_HARBOR'

# Secret per GitHub (usa Personal Access Token)
kubectl create secret generic github-creds -n argocd \
  --from-literal=username='utente' \
  --from-literal=token='IL_TUO_GITHUB_TOKEN'

# Verifica che i secret siano stati creati
kubectl get secrets -n argocd | grep -E "harbor-creds|github-creds"


dentro deyploment aggiungere piu application per fare piu imageupdates
APPLICATIONS="
flask-hello:michela877:flask-hello:test.local/michela877/flask-hello
nuova-app:michela877:nuovo-repo:test.local/michela877/nuova-app
"

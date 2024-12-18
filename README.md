### Setup Git Account
export GITHUB_USER=rajesh17mca
export GITHUB_TOKEN="PAT Token"

### Setup Flux bootstrap with github github
flux bootstrap github --owner=$GITHUB_USER --repository=flux-nginx-application --branch=main --path=flux-infra --personal

### Flux to create source git flux-nginx-application
flux create source git flux-nginx-application --url=https://github.com/rajesh17mca/flux-nginx-application.git --branch=main --interval=30s --export > ./nginx-app/flux_source.yaml

### Apply above source SOT using kustomization controller
flux create kustomization flux-nginx-application --source=flux-nginx-application --path="./nginx-app/" --prune=true --validation=client --interval=30s --export > ./flux-system/flux_sync.yaml

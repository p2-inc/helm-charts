
## Instructions for packaging helm charts

```
cd charts/keycloak
helm dependency build
cd ../..

helm lint charts/keycloak
helm package charts/keycloak

helm repo index --url https://p2-inc.github.io/helm-charts/ .
```
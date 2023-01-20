
## Instructions for packaging helm charts

```
cd charts/postgresql
helm repo update
helm dependency update
helm dependency build
cd ../..

cd charts/keycloak
helm repo update
helm dependency update
helm dependency build
cd ../..

helm lint charts/postgresql
helm package charts/postgresql

helm lint charts/keycloak
helm package charts/keycloak

helm repo index --url https://p2-inc.github.io/helm-charts/ --merge index.yaml .
```



## Deploy/Upgrade Locally


```
cd charts/keycloak
helm install keycloak --namespace keycloak --create-namespace .



helm upgrade -i keycloak --namespace keycloak .
```

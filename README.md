> :rocket: **Try it for free** in the new Phase Two [keycloak managed service](https://phasetwo.io/dashboard/?utm_source=github&utm_medium=readme&utm_campaign=helm-charts).

# The Phase Two Library for Kubernetes

[Phase Two](https://phasetwo.io) enhance [Keycloak](https://keycloak.org), ready to launch on Kubernetes using [Kubernetes Helm](https://github.com/helm/helm). This chart library was initially forked from [Bitnami](https://bitnami.com) and modified to deliver custom Phase Two enhanced Keycloak images.

## TL;DR (new helm repo)

```bash
$ helm repo add phasetwo https://p2-inc.github.io/helm-charts
$ helm install keycloak --namespace keycloak --create-namespace phasetwo/keycloak
$ kubectl get all,ing -n keycloak
```

## TL;DR (existing helm repo/release)

```bash
$ helm repo update
$ helm upgrade keycloak --namespace keycloak phasetwo/keycloak
$ kubectl get all,ing -n keycloak
```

## Enabling Metrics and Installing Prometheus and Grafana

To install Keycloak Metrics Exporter, Prometheus, Grafana, and Loki using Helm charts, you can use the following commands:

1. Update your values.yaml file to enable `metrics > enabled: true`

2. Upgrade your existing helm release:

```
helm upgrade -i keycloak --namespace keycloak phasetwo/keycloak
```

3. Add the Helm chart repository for Prometheus, Grafana, and Loki:

```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm search repo grafana
helm search repo prometheus-community
```

4. Use Helm to install the Prometheus, Grafana, and Loki charts:

```
helm install prometheus --namespace grafana --create-namespace prometheus-community/prometheus
helm install grafana --namespace grafana --create-namespace grafana/grafana --set persistence.enabled=true
helm install loki --namespace grafana --create-namespace grafana/loki
```

Please note that the above commands are just examples and you may want to customize the installation by passing in different values for the different chart options available.

You can also use the command `helm list` to check the status of the installed charts, and `helm delete my-release` to delete the specific installation.

## Gotchas

 * If you're running Kubernetes locally (eg. microk8s/minikube) and postgres is not starting, you may need to [disable huge pages](https://github.com/kubernetes/kubernetes/issues/71233#issuecomment-447472125). 

## Before you begin

### Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

### Setup a Kubernetes Cluster

For setting up Kubernetes on cloud platforms or bare-metal servers refer to the Kubernetes [getting started guide](https://kubernetes.io/docs/getting-started-guides/).

### Install Helm

Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

To install Helm, refer to the [Helm install guide](https://github.com/helm/helm#install) and ensure that the `helm` binary is in the `PATH` of your shell.

### Add Repo

The following command allows you to download and install all the charts from this repository:

```bash
$ helm repo add phasetwo https://p2-inc.github.io/helm-charts
```

### Using Helm

Once you have installed the Helm client, you can deploy a Bitnami Helm Chart into a Kubernetes cluster.

Please refer to the [Quick Start guide](https://helm.sh/docs/intro/quickstart/) if you wish to get running in just a few commands, otherwise the [Using Helm Guide](https://helm.sh/docs/intro/using_helm/) provides detailed instructions on how to use the Helm client to manage packages on your Kubernetes cluster.

Useful Helm Client Commands:
* View available charts: `helm search repo`
* Install a chart: `helm install my-release phasetwo/<package-name>`
* Upgrade your application: `helm upgrade`

## License

Copyright &copy; 2023 Phase Two, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

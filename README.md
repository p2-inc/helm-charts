[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/bitnami)](https://artifacthub.io/packages/search?repo=bitnami)
[![CD Pipeline](https://github.com/bitnami/charts/actions/workflows/cd-pipeline.yml/badge.svg)](https://github.com/bitnami/charts/actions/workflows/cd-pipeline.yml)

# The Phase Two Library for Kubernetes

Popular applications, provided by [Phase Two](https://phasetwo.io), ready to launch on Kubernetes using [Kubernetes Helm](https://github.com/helm/helm). This chart library was initially forked from [Bitnami](https://bitnami.com) and modified to deliver custom Phase Two keycloak images.

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

## Vulnerabilities scanner

Each Helm chart contains one or more containers. Those containers use images provided by Bitnami through its test & release pipeline and whose source code can be found at [bitnami/containers](https://github.com/bitnami/containers).

As part of the container releases, the images are scanned for vulnerabilities, [here](https://github.com/bitnami/containers#vulnerability-scan-in-bitnami-container-images) you can find more info about this topic.

Since the container image is an immutable artifact that is already analyzed, as part of the Helm chart release process we are not looking for vulnerabilities in the containers but running different verification to ensure the Helm charts work as expected, see the testing strategy defined at [_TESTING.md_](https://github.com/bitnami/charts/blob/main/TESTING.md).

## Before you begin

### Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

### Setup a Kubernetes Cluster

The quickest way to setup a Kubernetes cluster to install Bitnami Charts is following the "Bitnami Get Started" guides for the different services:

- [Get Started with Bitnami Charts using VMware Tanzu Kubernetes Grid](https://docs.bitnami.com/kubernetes/get-started-tkg/)
- [Get Started with Bitnami Charts using VMware Tanzu Mission Control](https://docs.bitnami.com/tutorials/tanzu-mission-control-get-started/)
- [Get Started with Bitnami Charts using the Azure Kubernetes Service (AKS)](https://docs.bitnami.com/kubernetes/get-started-aks/)
- [Get Started with Bitnami Charts using the Amazon Elastic Container Service for Kubernetes (EKS)](https://docs.bitnami.com/kubernetes/get-started-eks/)
- [Get Started with Bitnami Charts using the Google Kubernetes Engine (GKE)](https://docs.bitnami.com/kubernetes/get-started-gke/)
- [Get Started with Bitnami Charts using the IBM Cloud Kubernetes Service (IKS)](https://docs.bitnami.com/kubernetes/get-started-charts-iks/)

For setting up Kubernetes on other cloud platforms or bare-metal servers refer to the Kubernetes [getting started guide](https://kubernetes.io/docs/getting-started-guides/).

### Install Helm

Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

To install Helm, refer to the [Helm install guide](https://github.com/helm/helm#install) and ensure that the `helm` binary is in the `PATH` of your shell.

### Add Repo

The following command allows you to download and install all the charts from this repository:

```bash
$ helm repo add phasetwo https://p2-inc.github.io/helm-charts
```

> **_NOTE:_** It is important to note that the above mentioned repo is truncated so it only contains entries for the releases produced in the last 6 months. In case you need a full index, you can use it from the [archive-full-index branch](https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami/index.yaml) in the bitnami/charts Github repository.
>
> This full index is updated every time the [truncated index file](https://raw.githubusercontent.com/bitnami/charts/index/bitnami/index.yaml) is updated. Take into account that this full index is under the [Github's rate limits](https://docs.github.com/en/developers/apps/building-github-apps/rate-limits-for-github-apps).
>
> You can find more information in the [Bitnami index FAQ](https://github.com/bitnami/charts/issues/10833) pinned issue.

### Using Helm

Once you have installed the Helm client, you can deploy a Bitnami Helm Chart into a Kubernetes cluster.

Please refer to the [Quick Start guide](https://helm.sh/docs/intro/quickstart/) if you wish to get running in just a few commands, otherwise the [Using Helm Guide](https://helm.sh/docs/intro/using_helm/) provides detailed instructions on how to use the Helm client to manage packages on your Kubernetes cluster.

Useful Helm Client Commands:
* View available charts: `helm search repo`
* Install a chart: `helm install my-release phasetwo/<package-name>`
* Upgrade your application: `helm upgrade`

## License

Copyright &copy; 2022 Phase Two, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

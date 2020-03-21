# grafana_helm_values

<!-- TOC -->

- [grafana_helm_values](#grafanahelmvalues)
- [About](#about)
  - [Contributing](#contributing)
  - [Credits](#credits)
  - [Developers](#developers)
  - [License](#license)
- [Prerequisites to Development and Test of Helm Charts](#prerequisites-to-development-and-test-of-helm-charts)
- [How to Deploy Grafana in Kubernetes with Helm](#how-to-deploy-grafana-in-kubernetes-with-helm)

<!-- TOC -->

# About

My Helm Values for deploy of Grafana with Helm Charts developed by Bitnami.

## Contributing

Visit https://github.com/aeciopires/my_helm_charts

## Credits

Team Bitnami. Visit: 

* https://bitnami.com
* https://bitnami.com/stack/grafana/helm
* https://github.com/bitnami/charts/tree/master/bitnami/grafana

## Developers

developer: Aécio dos Santos Pires<br>
mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Prerequisites to Development and Test of Helm Charts

Visit https://github.com/aeciopires/my_helm_charts

# How to Deploy Grafana in Kubernetes with Helm

Create or access cluster Kubernetes and configure the kubectl.

Install Helm 3 (visit https://github.com/aeciopires/my_helm_charts).

Install plugin Helm secrets.

```bash
helm plugin install https://github.com/futuresimple/helm-secrets
```

Download repo charts of Bitnami.

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Execute Helm Update if repo bitnami is installed.

```bash
helm repo update
```

Download and configure the parameters for deploy of Grafana.

```bash
cd ~
git clone https://github.com/aeciopires/my_helm_charts.git
```

List the namespaces of cluster.

```bash
kubectl get namespaces
```

Create the namespaces ``monitoring`` if not exists in cluster.

```bash
kubectl create namespace monitoring
```

Deploy Grafana with Helm in cluster Kubernetes.

```bash
helm secrets upgrade grafana \
 -f ~/my_helm_charts/monitoring/grafana/minikube/values.yaml \
 -f ~/my_helm_charts/monitoring/grafana/minikube/secrets.yaml \
 bitnami/grafana \
 -n monitoring --install
```

View the pods of Grafana.

```bash
kubectl get pods -n monitoring
```

View informations of service Grafana.

```bash
kubectl describe deployments grafana -n monitoring
kubectl describe svc/grafana -n monitoring
```

View informations of pod Grafana.

```bash
kubectl describe deployments grafana -n monitoring
```

View the logs of Grafana.

```bash
kubectl logs -f svc/grafana -n monitoring
```

Access prompt of container of Grafana.

```bash
kubectl exec -it svc/grafana -n monitoring -- sh
```

The URL, login and password will show after deploy of Grafana. Follow the instructions.


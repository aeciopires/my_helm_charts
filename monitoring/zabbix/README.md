# zabbix_helm_values

<!-- TOC -->

- [zabbix_helm_values](#zabbixhelmvalues)
- [About](#about)
  - [Contributing](#contributing)
  - [Credits](#credits)
  - [Developers](#developers)
  - [License](#license)
- [Prerequisites to Development and Test of Helm Charts](#prerequisites-to-development-and-test-of-helm-charts)
- [How to Deploy Zabbix in Kubernetes](#how-to-deploy-zabbix-in-kubernetes)

<!-- TOC -->

# About

My Helm Values for deploy of Zabbix with Helm Charts.

There is still no stable Helm Chart for the production environment, so i'm using a version in development.

## Contributing

Visit https://github.com/aeciopires/my_helm_charts

## Credits

Contribuitora of GitHub Repo https://github.com/cetic/helm-zabbix

## Developers

developer: Aécio dos Santos Pires<br>
mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Prerequisites to Development and Test of Helm Charts

Visit https://github.com/aeciopires/my_helm_charts

# How to Deploy Zabbix in Kubernetes

Create or access cluster Kubernetes and configure the kubectl.

Install Helm 3 (visit https://github.com/aeciopires/my_helm_charts).

Install plugin Helm secrets.

```bash
helm init
helm plugin install https://github.com/futuresimple/helm-secrets
```

Download and configure the parameters for deploy of Zabbix.

```bash
cd ~
git clone https://github.com/aeciopires/my_helm_charts.git
```

Download of code of Helm Chart.

```bash
cd ~
git clone https://github.com/cetic/helm-zabbix
cd helm-zabbix
git checkout develop
```

Download dependences charts.

```bash
helm repo add stable https://kubernetes-charts-incubator.storage.googleapis.com/
helm repo update
cd ~/helm-zabbix
helm dependency update
```

List the namespaces of cluster.

```bash
kubectl get namespaces
```

Create the namespaces ``monitoring`` if not exists in cluster.

```bash
kubectl create namespace monitoring
```

Deploy Zabbix in cluster Kubernetes.

```bash
helm secrets upgrade zabbix \
 -f ~/my_helm_charts/monitoring/zabbix/minikube/values.yaml \
 -f ~/my_helm_charts/monitoring/zabbix/minikube/secrets.yaml \
 ~/helm-zabbix -n monitoring --install
```

View the pods.

```bash
kubectl get pods -n monitoring
```

View informations of pods.

```bash
kubectl describe pods/NAME_POD -n monitoring
```

View all containers of pod.

```bash
kubectl get pods NAME_POD -n monitoring -o jsonpath='{.spec.containers[*].name}*'
```

View the logs container of pods.

```bash
kubectl logs -f pods/NAME_POD -c NAME_CONTAINER -n monitoring
```

Access prompt of container.

```bash
kubectl exec -it pods/NAME_POD -c NAME_CONTAINER -n monitoring -- sh
```

View informations of service Grafana.

```bash
kubectl get svc
kubectl get pods --output=wide -n monitoring
kubectl describe services zabbix -n monitoring
```

Access Zabbix in http://IP-SERVER:80. Login ``Admin`` and password ``zabbix``.


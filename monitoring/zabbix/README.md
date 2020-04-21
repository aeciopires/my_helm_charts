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

Contribuitors of GitHub Repo https://github.com/cetic/helm-zabbix

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
helm plugin install https://github.com/futuresimple/helm-secrets
```

Download and configure the parameters for deploy of Zabbix.

```bash
cd ~
git clone https://github.com/aeciopires/my_helm_charts.git
```

Edit ``my_helm_charts/monitoring/zabbix/minikube/values.yaml`` file.

Edit ``my_helm_charts/monitoring/zabbix/minikube/secrets.yaml`` file with follow command or create your file of secrets and encrypt with ``helm secrets enc PATH_FILE_SECRETS`` command (see https://github.com/zendesk/helm-secrets). Where ``PATH_FILE_SECRETS`` must be replaced with the path to your new secrets file.

```bash
helm secrets edit my_helm_charts/monitoring/zabbix/minikube/secrets.yaml
```

| Properties in secret.yaml file        | Default Values |
|:--------------------------------------|:---------------|
| zabbixServer.POSTGRES_PASSWORD        | zabbix         |
| zabbixproxy.MYSQL_PASSWORD            | zabbix         |
| postgresql.postgresqlPassword         | zabbix         |
| postgresql.postgresqlPostgresPassword | rootpasswd     |
| zabbixweb.POSTGRES_PASSWORD           | zabbix         |

Download dependences charts.

```bash
helm repo add stable https://kubernetes-charts-incubator.storage.googleapis.com
helm repo add cetic https://cetic.github.io/helm-charts
helm repo update
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
helm secrets install zabbix \
 -f ~/my_helm_charts/monitoring/zabbix/minikube/values.yaml \
 -f ~/my_helm_charts/monitoring/zabbix/minikube/secrets.yaml \
 cetic/zabbix -n monitoring --install
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

Listen on port 8888 locally, forwarding to 80 in the pod

```bash
kubectl port-forward deployment/zabbix-web 8888:80 -n monitoring
```

Access Zabbix in http://localhost:8888. Login ``Admin`` and password ``zabbix``.

To uninstall the zabbix.

```bash
helm delete zabbix -n monitoring
```
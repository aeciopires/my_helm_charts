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

There is still no stable Helm Chart for the production environment, so I am using a definition shared by the Zabbix team.

## Contributing

Visit https://github.com/aeciopires/my_helm_charts

## Credits

Zabbix team and contribuitor of GitHub Repo https://github.com/cetic/helm-zabbix

* https://github.com/cetic/helm-zabbix
* https://raw.githubusercontent.com/zabbix/zabbix-docker/4.4/kubernetes.yaml

## Developers

developer: Aécio dos Santos Pires<br>
mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Prerequisites to Development and Test of Helm Charts

Visit https://github.com/aeciopires/my_helm_charts

# How to Deploy Zabbix in Kubernetes

Create or access cluster Kubernetes and configure the kubectl.

Download and custom configure the parameters for deploy of Zabbix.

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

Deploy Zabbix in cluster Kubernetes.

```bash
kubectl appy -f ~/my_helm_charts/monitoring/zabbix/minikube/kubernetes_zabbix.yaml
```

View the pods.

```bash
kubectl get pods -n monitoring
```

View informations of pods.

```bash
kubectl describe pods/NAME_POD -n monitoring
```

View the logs of pods.

```bash
kubectl logs -f pods/NAME_POD -n monitoring
```

Access prompt of container.

```bash
kubectl exec -it pods/NAME_POD -n monitoring -- sh
```

Access Zabbix in http://localhost:80. Login ``Admin`` and password ``zabbix``.


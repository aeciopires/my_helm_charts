# influxdb_chart

<!-- TOC -->

- [influxdb_chart](#influxdbchart)
- [About](#about)
  - [Contributing](#contributing)
  - [Developers](#developers)
  - [License](#license)
- [Commands to generate Helm Chart](#commands-to-generate-helm-chart)
- [Commands to publish Helm Chart](#commands-to-publish-helm-chart)
  - [Helm repo with support S3 in AWS.](#helm-repo-with-support-s3-in-aws)
  - [Helm repo with support GCS in GCP.](#helm-repo-with-support-gcs-in-gcp)
- [Commands to install my Helm Chart of InfluxDB](#commands-to-install-my-helm-chart-of-influxdb)

<!-- TOC -->

# About

My first Helm chart of InfluxDB for Kubernetes.

    ATTENTION: Created this chart for learning purposes only. To install InfluxDB using the official Helm Chart visit https://github.com/influxdata/helm-charts

## Contributing

See instructions in [README](https://github.com/aeciopires/my_helm_charts/blob/master/README.md)

## Developers

Developer: Aécio dos Santos Pires<br>
Mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Commands to generate Helm Chart

Creating my chart of influxdb.

```bash
cd my_helm_charts/monitoring

helm create influxdb
```

Lint sintax chart of influxdb.

```bash
my_helm_charts/monitoring

helm lint influxdb
```

Package chart of influxdb.

```bash
my_helm_charts/monitoring

helm package influxdb
```

# Commands to publish Helm Chart

## Helm repo with support S3 in AWS.

* https://github.com/hypnoglow/helm-s3
* https://medium.com/@ryan.gartin/private-helm-repository-aws-s3-terraform-69464080a643

Install plugin.

```bash
helm plugin install https://github.com/hypnoglow/helm-s3.git
```

To create a new repository, use init:

```bash
helm s3 init s3://myhelmcharts.myenvtest.com/charts
```

This command generates an empty `index.yaml` and uploads it to the S3 bucket under `/charts` key.

To work with this repo by it's name, first you need to add it using native helm command:

```bash
helm repo add myhelmcharts_s3 s3://myhelmcharts.myenvtest.com/charts
```

Now you can push your chart to this repo.

```bash
helm s3 push ./influxdb-0.1.0.tgz myhelmcharts_s3
```

On push, both remote and local repo indexes are automatically updated (that means you don't need to run ``helm repo update``).

Your pushed chart is available:

```bash
helm search repo myhelmcharts
```

More informations usage in https://github.com/hypnoglow/helm-s3

---

Credits: Igor Zibarev hypnoglow@gmail.com

https://github.com/hypnoglow/helm-s3

---

## Helm repo with support GCS in GCP.

* https://github.com/hayorov/helm-gcs

Install plugin.

```bash
helm plugin install https://github.com/hayorov/helm-gcs
```

Init a new repository.

```bash
helm gcs init gs://myhelmcharts --service-account ~/.gcp/NOME_FILE.json
```

Add your repository to Helm.

```bash
helm repo add myhelmcharts_gcs gs://myhelmcharts
```

Push a chart to your repository.

```bash
helm gcs push ./influxdb-0.1.0.tgz myhelmcharts_gcs
```

Update Helm cache.

```bash
helm repo update
```

Get your chart.

```bash
helm fetch myhelmcharts_gcs/influxdb-0.1.0.tgz 
```

More information usage in https://github.com/hayorov/helm-gcs

---

Credits: Igor Zibarev hypnoglow@gmail.com

https://github.com/hayorov/helm-gcs

---

# Commands to install my Helm Chart of InfluxDB


Download and configure the parameters for deploy of InfluxDB.

```bash
cd ~
git clone https://github.com/aeciopires/my_helm_charts.git
```

Edit ``my_helm_charts/monitoring/influxdb/values.yaml`` file.

List the namespaces of cluster.

```bash
kubectl get namespaces
```

Create the namespaces ``monitoring`` if not exists in cluster.

```bash
kubectl create namespace monitoring
```

Deploy InfluxDB with my Helm Chart in Kubernetes cluster.

```bash
helm install influxdb  -f ~/my_helm_charts/monitoring/influxdb/values.yaml ~/my_helm_charts/monitoring/influxdb  -n monitoring
```

View the pods of InfluxDB.

```bash
kubectl get pods -n monitoring
```

View informations of deployment and InfluxDB service.

```bash
kubectl describe deployments influxdb -n monitoring
kubectl describe svc/influxdb -n monitoring
```

View the logs of InfluxDB.

```bash
kubectl logs -f svc/influxdb -n monitoring
kubectl logs -f pods/NAME_POD -n monitoring
```

Access prompt of container of InfluxDB.

```bash
kubectl exec -it svc/influxdb -n monitoring -- sh
```

Listen on port 8080 locally, forwarding to 9999 in the pod.

```bash
kubectl port-forward svc/influxdb 8080:9999 -n monitoring
```

Access InfluxDB in http://localhost:8080.

To uninstall the InfluxDB.

```bash
helm delete influxdb -n monitoring
```
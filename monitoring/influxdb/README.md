# influxdb_chart

<!-- TOC -->

- [influxdb_chart](#influxdbchart)
- [About](#about)
  - [Contributing](#contributing)
  - [Developers](#developers)
  - [License](#license)
- [Commands to Generate Helm Chart](#commands-to-generate-helm-chart)
- [Commands to Publish Helm Chart](#commands-to-publish-helm-chart)
  - [Helm repo with support S3 in AWS.](#helm-repo-with-support-s3-in-aws)
  - [Helm repo with support GCS na GCP.](#helm-repo-with-support-gcs-na-gcp)

<!-- TOC -->

# About

My first Helm Charts of InfluxDB for Kubernetes.

## Contributing

See instructions in [README](https://github.com/aeciopires/my_helm_charts/blob/master/README.md)

## Developers

developer: Aécio dos Santos Pires<br>
mail: http://blog.aeciopires.com/contato

## License

GPL-3.0 2020 Aécio dos Santos Pires

# Commands to Generate Helm Chart

Create a chart

```bash
cd my_helm_charts/monitoring

helm create NAME_CHART
```

Lint sintax chart

```bash
my_helm_charts/monitoring

helm lint NAME_CHART
```

Package chart

```bash
my_helm_charts/monitoring

helm package NAME_CHART
```

# Commands to Publish Helm Chart

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
helm repo add myhelmcharts s3://myhelmcharts.myenvtest.com/charts
```

Now you can push your chart to this repo.

```bash
helm s3 push ./influxdb-0.1.0.tgz myhelmcharts
```

On push, both remote and local repo indexes are automatically updated (that means you don't need to run helm repo update).

Your pushed chart is available:

```bash
helm search repo myhelmcharts
```

More informations usage in https://github.com/hypnoglow/helm-s3

---

Credits: Igor Zibarev hypnoglow@gmail.com

https://github.com/hypnoglow/helm-s3

---

## Helm repo with support GCS na GCP.

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
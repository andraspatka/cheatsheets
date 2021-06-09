# Helm cheatsheet

## Repositories

Add repository:
```bash
helm repo add <name> <url>
```

List all repositories:
```bash
helm repo list
```

Search for an artifact:

```bash
# Searches for artifact in Artifact hub (https://artifacthub.io/)
helm search hub <name>

# Searches in the configured repos
helm search repo <name>
```

## View information about a chart

```bash
# e.g. add bitnami repository 
helm repo add bitnami https://charts.bitnami.com/bitnami
# get information about the bitnami mongodb chart
helm show chart bitnami/mongodb
# show the chart's values.yaml
helm show values bitnami/mongodb
```

## Installing and managing charts

Updating a chart's dependencies:

```bash
helm dependency update
```

Simulate an install (interacts with the K8s API, checks if object already exist, etc.):

```bash
helm install --dry-run ...
```

Install a chart by a reference:

```bash
helm install mongodb bitnami/mongodb
```

Install chart from packaged file

```bash
helm install <deployment_name> <path_to_packaged_chart>.tgz
```

Install chart from unpackaged file

```bash
helm install <deployment_name> <path_to_chart_directory>
```

Install chart and override values from template with a yaml file:

```bash
helm install -f ./extra-values.yml ./chart
```

Install chart and override specific values:

```bash
helm install --set key1=value1,key2=value2 <deployment_name> <chart>
```

## Getting information about deployed charts

List all releases:

```bash
helm list
```

See all objects created by a release:

```bash
helm get manifest <release_name>
```

Get status message of a release:

```bash
helm status <release_name>
```

## Uninstall a chart

```bash
helm uninstall <release_name>
```

## Developing charts

Creating a chart - skeleton project, contains all the boilerplate which is needed to get started with a helm chart:

```bash
helm create <chart_name>
```

Locally render a chart template - useful for finding problems with the templates

```bash
helm template <path_to_chart>
```

# Helm Charts

Download the dependency charts

```bash
helm dependency update charts/graphile-postgres
```

Build the charts

```bash
helm package --destination ./dist charts/*
```

Create the index file.

```bash
helm repo index --merge index.yaml --url https://charts.jtco.io .
```

Add the repo locally

```bash
helm repo add jtco https://charts.jtco.io 
```

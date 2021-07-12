# Helm Charts

First we need to download the dependency charts

```bash
helm dependency update charts/graphile-postgres
```

Next lets build the charts

```bash
helm package --destination ./dist charts/*
```

Finally lets create our index

```
helm repo index --url https://charts.jtco.io .
```

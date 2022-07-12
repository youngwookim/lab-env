# OpenSearch

```
helm repo add opensearch https://opensearch-project.github.io/helm-charts/
helm repo update

helm search repo opensearch --versions

# https://github.com/opensearch-project/helm-charts/issues/87
```


-- opensearch
```
helm upgrade --install -n opensearch opensearch opensearch/opensearch -f values-os.yaml \
--create-namespace

-- opensearch-dashboards
helm upgrade --install -n opensearch opensearch-dashboards opensearch/opensearch-dashboards --create-namespace
```

Refs.
- https://opensearch.org/blog/technical-post/2022/05/opentelemetry-metrics-for-data-prepper/
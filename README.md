To set scrape config for prometheus deployed in k8s cluster first , you will need to create the additional configuration. For instance
```
job_name: "pushgateway"
  static_configs:
  - targets: ["prometheus-pushgateway:9091"]
```
Then make a secret of it:
```
kubectl create secret generic additional-scrape-configs --from-file=prometheus-additional.yaml --dry-run=client -oyaml > additional-scrape-configs.yaml
```
And now, apply the generated manifest:
```
kubectl apply -f additional-scrape-configs.yaml -n monitoring
```
Then find prometheus components in the name space
```
kubectl get Prometheus -n monitoring
```
And edit CRD 
```
kubectl edit Prometheus kube-prometheus-stack-prometheus -n monitoring
```
Finally refrence this additional configuration under spec section:
```
additionalScrapeConfigs:
    name: additional-scrape-configs
    key: prometheus-additional.yaml
```



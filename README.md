To set scrape config for prometheus deployed in k8s cluster first , you will need to create the additional configuration. For instance
```
job_name: "pushgateway"
  static_configs:
  - targets: ["prometheus-pushgateway:9091"]
```


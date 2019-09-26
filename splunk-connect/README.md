
```helm install --name my-splunk-objects -f objects.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-objects-1.2.0.tgz```

```helm upgrade my-splunk-metrics  --install -f metrics.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-metrics-1.2.0.tgz```

```helm upgrade my-splunk-logging --install -f logging.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-logging-1.2.0.tgz```

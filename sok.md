=== installation ===

```
kubectl apply -f https://github.com/splunk/splunk-operator/releases/download/0.2.0/splunk-operator-install.yaml --namespace=splunk
```


=== uninstall ===

```
kubectl delete standalones --all
kubectl delete licensemasters --all
kubectl delete searchheadclusters --all
kubectl delete indexerclusters --all
kubectl delete spark --all

kubectl delete clustermasters --all
kubectl delete -f https://github.com/splunk/splunk-operator/releases/download/0.2.0/splunk-operator-install.yaml
```
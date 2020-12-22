=== installation ===

```
k create ns splunk
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

- get admin password
```
kubectl get secret splunk-splunk-secret -o jsonpath='{.data.password}' | base64 --decode
```


### custom resources ###

- documentation
https://github.com/splunk/splunk-operator/blob/master/deploy/crds/enterprise.splunk.com_licensemasters_crd.yaml

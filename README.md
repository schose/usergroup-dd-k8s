
### tools needed ###

  

- eksctl -> https://eksctl.io/

  

### create EKS Cluster

  

- create cluster control plane

``eksctl create cluster -f ./aws/aws-cluster.yaml``

  

- create nodegroup

  

``eksctl create nodegroup --cluster splunkusergroup --name nodes --node-zones=eu-central-1a --nodes 3 --node-type m5.2xlarge``

  

oder

  

``eksctl create nodegroup --config-file=./aws/aws-cluster.yaml --include=ng-1``

  

- temporarily delete nodegroup

  

``eksctl delete nodegroup nodess --cluster splunkusergroup ``

  

### prepair kubectl

  

- update kubectl config

``aws eks --region eu-central-1 update-kubeconfig --name splunkusergroup``

  
  

### deploy

  

- install configmaps

  

``k apply -f prep/splunk-configmap.yml``
``k apply -f prep/splunk-defaults-configmap.yml``

  

- create storage claims

  

``k apply -f pvc``

  

- create services

  

``k apply -f services``

  

- create pods

  

``k apply -f deploy``

  

- create ALB loadbalancer for internet connectivity

  

``k apply -f alb``

  
  





  


  

and change permissions manually

  

### Links

  

- in-deep description of defaults.yml

  

https://github.com/splunk/splunk-ansible/blob/develop/docs/advanced/default.yml.spec.md

    

### do hec test

```curl -k https://hec.bwlab.de/services/collector -H 'Authorization: Splunk d8d17157-a4d3-4bb2-98cd-e636c5e88811' -d '{"event":"Hello, World!"}'```


### Helm

- install

```helm init --service-account=tiller --history-max 200```

```help apply -f rbac.yml```

```kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default```

  

### install Splunk connect for Kubernetes


``helm install --name my-splunk-objects -f objects.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-objects-1.2.0.tgz``
  
``helm upgrade my-splunk-metrics --install -f metrics.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-metrics-1.2.0.tgz``

``helm upgrade my-splunk-logging --install -f logging.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-kubernetes-logging-1.2.0.tgz``

### Issues and further reading

- https://github.com/splunk/splunk-ansible/pull/211/commits
- permission denied error when upgrading from 7.2.6
workaround:

- start container with

`` command: ['sh', '-c', 'echo The app is running! && sleep 3600']``

- should be fixed at 7.3.1

- ansible ENV variables [https://splunk.github.io/splunk-ansible/ADVANCED.html#inventory-script](https://splunk.github.io/splunk-ansible/ADVANCED.html)
- •[https://github.com/splunk/splunk-connect-for-kubernetes](https://github.com/splunk/splunk-connect-for-kubernetes)
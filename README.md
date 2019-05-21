# This Repository contains the WSO2 Product Suite which can be deployed in the Kubernetes Cluster with little configuration

## Usage:-
The applications are available at the respective NodePorts can be found my look at the service endpoints.Remember to put **https://** before WSO2 Product URLs.

### To start the Kubernetes WSO2 Product Stack

```kubectl create -f wso2-app.yml```

### To stop the Kubernetes WSO2 Product Stack

```kubectl delete -f wso2-app.yml```

## Required Configuration :-

#### Kubernetes configuration

```
vi ~/.kube/config

kind: Config
clusters:
- cluster:
    api-version: v1
    insecure-skip-tls-verify: true
    server: "http://rancher-dev.techienation.in:8080/r/projects/1a7/kubernetes"
  name: "kubernetes-dev"
contexts:
- context:
    cluster: "kubernetes-dev"
    user: "kubernetes-dev"
  name: "kubernetes-dev"
current-context: "kubernetes-dev"
users:
- name: "kubernetes-dev"
  user:
    username: "177D8B97B7470A5F26E5"
    password: "dofpPHcqioq4J4DqVA5U2Zp33d7HtayKhXBHV9vr"
```

##### (Optional) if Secret is not provided for the private registry

```
kubectl create secret docker-registry privateregistry --docker-server=hub.docker.com  --docker-username=<username> --docker-password=<password> --docker-email=<email_id>
```


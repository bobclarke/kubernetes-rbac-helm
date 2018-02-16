# Experimenting with Helm to manage RBAC roles and rolebindings


Work in progress 

# Notes
* Enable RBAC on our k8s cluster (if using minikube this is done as follows: `__minikube start --extra-config=apiserver.Authorization.Mode=RBAC__`) 
* Add a service user bind that user to the k8s cluster-admin role by running `kubectl create -f` on the manifest below:
```
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system

```
* Next, initialise heml with `helm init --service-account tiller `
* Create a couple of namespaces on your cluster for each test project. I'm using project-001, project 002 etc
* Now you're ready to run this test chart. Clone this repo and run 
```
helm upgrade project-001 rbac-test --install --values rbac-test/project/project.yaml --dry-run --debug
```


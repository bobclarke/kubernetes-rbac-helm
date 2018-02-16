# Experimenting with Helm to manage RBAC roles and rolebindings


Work in progress 

# Notes
* Enable RBAC on our k8s cluster (if using minikube this is done as follows: __minikube start --extra-config=apiserver.Authorization.Mode=RBAC__) 
* Add a service user bind that user to the k8s cluster-admin role as follows:
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


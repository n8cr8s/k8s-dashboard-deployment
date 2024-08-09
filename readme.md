# Deploy K8s Dashboard

```
# Add kubernetes-dashboard repository
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
# Deploy a Helm Release named "kubernetes-dashboard" using the kubernetes-dashboard chart
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard

```
## Create user

```
kubectl apply -f dashboard-user.yaml
```

## Generate Token

Do one of the following

### Temp Token

```
kubectl -n kubernetes-dashboard create token admin-user
```

### Get long generated token 

```
kubectl apply -f token.yaml
kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath={".data.token"} | base64 -d
```


## Start Proxy
```
kubectl proxy
```

Go to browser and open http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
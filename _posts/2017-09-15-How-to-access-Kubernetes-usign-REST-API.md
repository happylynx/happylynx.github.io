# How to access Kubernetes using REST API

# Using proxy

```bash
kubectl proxy
# or to allow access from all interfaces
kubectl proxy --address=0.0.0.0 --accept-hosts='.*'
```

```
curl localhost:8001
````

# By passing token in request header

1. Get token from output of

   ```
   kubectl get secrets -o yaml
   ```

2. Get api url from output of 

   ```bash
   kubectl config view
   # OR
   kubectl cluster-info
   ```

   e.g. https://192.168.121.54:6443

3. Fire the request

   ```
   curl -k --header "Authorization: Bearer ${TOKEN}" ${API_URL}
   ```
---
Details in [Accessing Cluster](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/)


### hello-kube-pod.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-kube-pod
  namespace: default
spec:
  containers:
    - name: hello-kube
      image: dorako321/hello-kube
      ports:
        - containerPort: 8080
```

### hello-kube-deployment.yaml

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: hello-kube-deployment
  namespace: default
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: hello-kube-pod
    spec:
      containers:
      - name: hello-kube
        image: dorako321/hello-kube
        ports:
          - containerPort: 8080
```


### hello-kube-service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-kube-service
  namespace: default
spec:
  ports:
    - port: 8080
      protocol: TCP
      tartgetPort: 8080
  selector:
    app: hello-kube-pod
  type: ClusterIP
```

### hello-kube-ingress.yaml

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hello-kube-ingress
  namespace: default
spec:
  rules:
    - host: hello-kube.localhost
      http:
        paths:
          - backend:
              serviceName: hello-kube-service
              servicePort: 8080
```

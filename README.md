Run server:

```sh
deno run --allow-env --allow-net --unstable --watch app-run.js
```

# Steps to create a deployment in a Minikube cluster

Built an image for Minikube:

```sh
minikube image build -t minikube-demo-server:1.0 .
```

List minikube image ls:

```sh
minikube start
minikube image ls
```

Creating a deployment file then apply the deployment configuration to the Minikube cluster:

```sh
kubectl apply -f k8s/minikube-demo-server-deployment.yaml
```

Adding a service and accessing the deployment then apply the service configuration :

```sh
kubectl apply -f k8s/minikube-demo-server-service.yaml
```

Check the status of the deployment n service:

```sh
kubectl get all
```

Get the external IP address of the service

```sh
minikube service minikube-demo-server-service --url
curl http://192.168.49.2:32531
```

# Steps to update deployment

Update server/app.js, then rebuild image with

```sh
cd server
minikube image build -t minikube-demo-server:1.1 .
```

Modify the deployment config file, then apply the change:

```sh
cd ..
kubectl apply -f k8s/minikube-demo-server-deployment.yaml
```

# Roll back deployment

```sh
kubectl rollout undo deployment.apps/minikube-demo-server-deployment
```

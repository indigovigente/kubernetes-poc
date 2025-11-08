# kubernetes-poc

This project was developed with the goal of studying, practicing, and understanding how Kubernetes works, including its main components and operating patterns in distributed environments.

Concepts explored here include:

- Deployments
- Services (ClusterIP, NodePort, and LoadBalancer)
- ConfigMaps and Secrets
- Autoscaling
- Internal and external networking
- Minikube and minikube tunnel for service exposure

The focus of this repository is to serve as a learning, testing, and experimentation base, allowing you to understand how real-world applications can be structured, packaged, and executed in a Kubernetes cluster.

Feel free to use this project as a reference or starting point for your own studies.

## Defining environment variables

Create a file named `secrets.yaml` inside the `k8s` directory and define the following environment variables.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: senhas
type: Opaque
stringData:
  DB_PASSWORD: "<your_password_here>"
  DB_USER: "<your_username_here>"
```

## Minikube installation

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## Start minikube
```bash
minikube start
```

## Enable the driver for the native persistent volume provider in Minikube.
```bash
minikube addons enable csi-hostpath-driver 
```

## Kubectl installation
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

## Validate the Kubectl version.
```bash
kubectl version --client
```

## Apply the Kubernetes metadata file settings.
```bash
kubectl apply -f k8s/volumes.yaml -f k8s/mysql.yaml -f k8s/secrets.yaml -f k8s/configmap.yaml -f k8s/app.yaml -f k8s/loadbalancer.yaml -f k8s/services.yaml
```

## Running this command will cause Minikube to simulate load balancers by creating network tunnels.

```bash
minikube tunnel -bind-address=<your machine's IP address>
```

## List all the services that are being orchestrated by Kubernetes.

```bash
kubectl get svc
```

### Observation
> If you want to test, you can get the IP addresses of the load balancers created by Kubernetes and test by accessing the ports described in the applications.
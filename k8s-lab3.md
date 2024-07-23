## Kubernetes Services Lab: ClusterIP and NodePort

### Objective
Learn how to create and manage ClusterIP and NodePort services in Kubernetes.

### Prerequisites

- Kubernetes cluster access
- kubectl command-line tool installed and configured
- Basic understanding of Kubernetes and YAML

## Part 1: ClusterIP Service

### 1.1 Create a ClusterIP Service

**Create a Deployment for the Nginx Application**

Create a file named `nginx-deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

Apply the Deployment

```bash
kubectl apply -f nginx-deployment.yaml
```

**Create a ClusterIP Service**

Create a file named nginx-clusterip-service.yaml with the following content:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-clusterip-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80

```
**Apply the ClusterIP Service**

```bash
kubectl apply -f nginx-clusterip-service.yaml
```

**Verify the Service**

```bash
kubectl get services
```

**Access the Service**

Use a temporary Pod to test the ClusterIP service:

```bash
kubectl run curlpod --image=busybox -i --tty -- /bin/sh
```

Inside the curlpod, use the following command to access the Nginx service:

```bash
wget -qO- nginx-clusterip-service
```

Exit the Pod by typing exit.


## Part 2: NodePort Service

### 2.1 Create a NodePort Service

**Create a NodePort Service**

Create a file named nginx-nodeport-service.yaml with the following content:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30007
```
**Apply the NodePort Service**

```bash
kubectl apply -f nginx-nodeport-service.yaml
```

**Verify the Service**
```bash
kubectl get services
```

**Accessing the service**

The network is limited if using the Docker driver on Darwin, Windows, or WSL, and the Node IP is not reachable directly.

Running minikube on Linux with the Docker driver will result in no tunnel being created.

Services of type NodePort can be exposed via the minikube service <service-name> --url command.

```bash
minikube service nginx-nodeport-service --url
```

minikube service hello-minikube1 --url runs as a process, creating a tunnel to the cluster. The command exposes the service directly to any program running on the host operating system.

Now, curl the address appearing on your terminal on a different terminal, you should be able to access Nginx.

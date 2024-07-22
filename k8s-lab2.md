## Kubernetes Pods Lab

### Objective
Learn about Pods in Kubernetes by creating, inspecting, and managing them. This lab will guide you through the fundamental operations related to Pods.

### Prerequisites
- Kubernetes cluster access
- `kubectl` command-line tool installed and configured
- Basic understanding of Kubernetes and YAML

### Part 1: Understanding Pods

**1.1 What is a Pod?**

A Pod is the smallest deployable unit in Kubernetes. It can contain one or more containers that share the same network namespace, storage, and configuration. Pods enable tightly coupled application components to run together and share resources.

**1.2 Key Concepts:**
- **Single-container Pod:** A Pod with one container.
- **Multi-container Pod:** A Pod with multiple containers that share storage and networking.

### Part 2: Creating and Inspecting Pods

**2.1 Create a Simple Pod**

1. **Create a YAML file for a Pod.**

   Create a file named `nginx-pod.yaml` with the following content:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx-pod
   spec:
     containers:
     - name: nginx-container
       image: nginx:latest
       ports:
       - containerPort: 80
   ```

2. **Apply the YAML file to create the Pod.**

  ```bash
  kubectl apply -f nginx-pod.yaml
  ```

3. **Verify the Pod has been created.**

  ```bash
  kubectl get pods
  ```

You should see nginx-pod listed.

**2.2 Inspect the Pod**

**Get detailed information about the Pod.**

```bash
kubectl describe pod nginx-pod
```

This command provides detailed information about the Pod, including events, status, and container details.

**View the Pod’s YAML configuration.**

```bash
kubectl get pod nginx-pod -o yaml
```

This command shows the current configuration of the Pod in YAML format.

### Part 3: Managing Pods

**3.1 Access the Pod**

**Exec into the Pod to run commands inside it.**

```bash
kubectl exec -it nginx-pod -- /bin/bash
```

This command opens a shell inside the nginx-container of the Pod.

**3.2 Deleting a Pod**

Delete the Pod.

```bash
kubectl delete pod nginx-pod
```

This command deletes the Pod. Verify the deletion by listing Pods again:

```bash
kubectl get pods
```

### Part 4: Advanced Pod Configuration

**4.1 Multi-container Pod Example**

Create a YAML file for a multi-container Pod.

Create a file named multi-container-pod.yaml with the following content:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
  - name: busybox-container
    image: busybox
    command: ["sleep", "3600"]
```

***Apply the YAML file to create the multi-container Pod.***

```bash
kubectl apply -f multi-container-pod.yaml
```

***Inspect the multi-container Pod.***

```bash
kubectl describe pod multi-container-pod
```

***Verify that both containers are running within the Pod.***

**4.2 Resource Requests and Limits**

***Update the nginx-pod.yaml file to include resource requests and limits.***

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

***Apply the updated YAML file.***

```bash
kubectl apply -f nginx-pod.yaml
```

***Verify the resource configuration.***

```bash
kubectl describe pod nginx-pod
```

Know more about resource requests and limits -> https://sysdig.com/blog/kubernetes-limits-requests/

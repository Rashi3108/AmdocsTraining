## Part 1: Understanding Labels
### 1.1 What are Labels?

Labels are key-value pairs attached to Kubernetes objects, such as Pods, to organize and categorize them. Labels can be used to select and group objects, making it easier to manage and filter resources.

## Part 2: Creating and Managing Pods with Labels
### 2.1 Create a Pod with Labels

Create a YAML file for a Pod with labels.

**Create a file named labeled-pod.yaml with the following content:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: labeled-pod
  labels:
    app: my-app
    environment: development
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

In this YAML file, the Pod is labeled with app: my-app and environment: development.

Apply the YAML file to create the Pod.

```bash
kubectl apply -f labeled-pod.yaml
```

Verify the Pod has been created and has the labels.

```bash
kubectl get pods --show-labels
```

You should see labeled-pod listed with the labels app=my-app and environment=development.

### 2.2 Selecting Pods with Labels

List Pods with a specific label.

To list Pods with the label app=my-app, use:

```bash
kubectl get pods -l app=my-app
```

List Pods with multiple labels.

To list Pods with both app=my-app and environment=development, use:

```bash
kubectl get pods -l app=my-app,environment=development
```
List Pods with a label selector.

To list Pods with a label that matches a certain value or pattern, use:

```bash
kubectl get pods -l 'app in (my-app)'
```

## Part 3: Updating and Removing Labels
###3.1 Update Labels on a Pod

Add or update a label on an existing Pod.

Use the kubectl label command to add or update a label:

```bash
kubectl label pod labeled-pod version=v1
```

Verify the updated labels.

```bash
kubectl get pods --show-labels
```

You should see the updated labels including version=v1.

## 3.2 Remove a Label from a Pod

Remove a label from an existing Pod.

Use the kubectl label command with a - to remove a label:

```bash
kubectl label pod labeled-pod environment-
```

Verify the label removal.

```
kubectl get pods --show-labels
```

Check that the environment label has been removed.

## Part 4: Practical Exercise
### 4.1 Create Multiple Pods with Different Labels

Create YAML files for multiple Pods with different labels.

Create a file named multi-labeled-pods.yaml with the following content:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
  labels:
    app: my-app
    environment: staging
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

---

apiVersion: v1
kind: Pod
metadata:
  name: pod-2
  labels:
    app: my-app
    environment: production
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

```

Apply the YAML file to create the Pods.

```bash
kubectl apply -f multi-labeled-pods.yaml
```

Verify the creation and labeling of the Pods.

```bash
kubectl get pods --show-labels
```

Select Pods based on different label criteria.

List Pods with environment=staging:

```bash
kubectl get pods -l environment=staging
```
List Pods with app=my-app:

```bash
kubectl get pods -l app=my-app
```

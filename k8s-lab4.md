# Multiple Choice Questions on Pods, Services, Labels, and Selectors

### 1. What is the primary purpose of a Pod in Kubernetes?
- A. To manage and store data
- B. To provide load balancing for applications
- C. To run one or more containers
- D. To monitor system performance

### 2. Which Kubernetes object allows you to access a Pod from outside the cluster?
- A. Deployment
- B. Secret
- C. Service
- D. ConfigMap

### 3. What is the default service type in Kubernetes if not specified?
- A. LoadBalancer
- B. ClusterIP
- C. NodePort
- D. ExternalName

### 4. How do you check the status and events of a Pod?
- A. `kubectl get pods`
- B. `kubectl describe pod <pod-name>`
- C. `kubectl logs <pod-name>`
- D. `kubectl exec -it <pod-name> -- /bin/bash`

### 5. What type of Service is used to expose a Pod on a specific port across all nodes in the cluster?
- A. ClusterIP
- B. NodePort
- C. LoadBalancer
- D. ExternalName

### 6. Which command is used to create a Pod from a YAML file?
- A. `kubectl create -f <file-name>.yaml`
- B. `kubectl apply -f <file-name>.yaml`
- C. `kubectl deploy -f <file-name>.yaml`
- D. `kubectl run -f <file-name>.yaml`

### 7. How do you access the logs of a container running in a Pod?
- A. `kubectl exec <pod-name> -- cat /var/log/container.log`
- B. `kubectl logs <pod-name>`
- C. `kubectl describe pod <pod-name>`
- D. `kubectl get logs <pod-name>`

### 8. What is the purpose of the `nodePort` in a NodePort service?
- A. To specify the internal port of the Pod
- B. To allocate a port on each node for external access
- C. To define the target port for the container
- D. To map the service to a different namespace

### 9. What happens if you delete a Pod in Kubernetes?
- A. The Deployment will be deleted as well
- B. The Service will be deleted
- C. The Pod will be recreated if it is part of a ReplicaSet or Deployment
- D. The entire Node will be deleted

### 10. Which Kubernetes object defines a set of Pods with a specific label?
- A. ReplicaSet
- B. Service
- C. ConfigMap
- D. Namespace

### 11. What is the purpose of labels in Kubernetes?
- A. To assign security policies to Pods
- B. To manage and organize Kubernetes objects
- C. To define the internal network configuration
- D. To specify resource limits for containers

### 12. How does a Service use selectors to associate with Pods?
- A. By matching the Pod’s IP address
- B. By using labels assigned to Pods
- C. By querying the Pod’s logs
- D. By defining a set of fixed ports

### 13. Which command is used to add a label to an existing Pod?
- A. `kubectl label pod <pod-name> <key>=<value>`
- B. `kubectl add label pod <pod-name> <key>=<value>`
- C. `kubectl set label pod <pod-name> <key>=<value>`
- D. `kubectl modify pod <pod-name> --label <key>=<value>`

### 14. What happens if multiple Services have overlapping selectors in Kubernetes?
- A. All Services will be associated with the same Pods
- B. Only the first Service will be associated with the Pods
- C. Each Service will only use its own Pods, even if the selectors overlap
- D. An error will occur and no Services will be created

### 15. Which YAML snippet correctly defines a Service that selects Pods with the label `app: myapp`?
- A. 
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-service
  spec:
    selector:
      app: myapp
    ports:
      - protocol: TCP
        port: 80
        targetPort: 80

  ```

- B. 
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-service
  spec:
    labels:
      app: myapp
    ports:
      - protocol: TCP
        port: 80
        targetPort: 80
  ```

- C. 
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-service
  spec:
    selector:
      app: myapp
    ports:
      - protocol: TCP
        targetPort: 80
        port: 80
  ```

  - D. 
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-service
  spec:
    selector:
      name: myapp
    ports:
      - protocol: UDP
        port: 80
        targetPort: 80
  ```

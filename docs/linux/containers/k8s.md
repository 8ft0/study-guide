### Kubernetes Command Line Syntax Study Sheet

**Purpose**: To provide a quick reference for commonly used Kubernetes (kubectl) commands.

---

#### Basic Commands

1. **Get Information**:
    - **Get all pods**: 
      ```sh
      kubectl get pods
      ```
    - **Get all services**:
      ```sh
      kubectl get services
      ```
    - **Get all nodes**:
      ```sh
      kubectl get nodes
      ```
    - **Get all deployments**:
      ```sh
      kubectl get deployments
      ```

2. **Describe Resources**:
    - **Describe a pod**:
      ```sh
      kubectl describe pod <pod-name>
      ```
    - **Describe a node**:
      ```sh
      kubectl describe node <node-name>
      ```
    - **Describe a service**:
      ```sh
      kubectl describe service <service-name>
      ```

3. **Create Resources**:
    - **Create a pod from a YAML file**:
      ```sh
      kubectl create -f <file.yaml>
      ```
    - **Create a deployment**:
      ```sh
      kubectl create deployment <deployment-name> --image=<image-name>
      ```
    - **Expose a deployment as a service**:
      ```sh
      kubectl expose deployment <deployment-name> --port=<port> --target-port=<target-port>
      ```

4. **Update Resources**:
    - **Apply changes from a YAML file**:
      ```sh
      kubectl apply -f <file.yaml>
      ```
    - **Edit a resource (e.g., deployment)**:
      ```sh
      kubectl edit deployment <deployment-name>
      ```

5. **Delete Resources**:
    - **Delete a pod**:
      ```sh
      kubectl delete pod <pod-name>
      ```
    - **Delete a deployment**:
      ```sh
      kubectl delete deployment <deployment-name>
      ```
    - **Delete all pods in a namespace**:
      ```sh
      kubectl delete pods --all --namespace=<namespace>
      ```

#### Advanced Commands

1. **Logs and Debugging**:
    - **View pod logs**:
      ```sh
      kubectl logs <pod-name>
      ```
    - **Stream pod logs**:
      ```sh
      kubectl logs -f <pod-name>
      ```
    - **Execute a command in a pod**:
      ```sh
      kubectl exec -it <pod-name> -- <command>
      ```

2. **Scaling**:
    - **Scale a deployment**:
      ```sh
      kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>
      ```

3. **Configuration and Context**:
    - **View current context**:
      ```sh
      kubectl config current-context
      ```
    - **Set a context**:
      ```sh
      kubectl config use-context <context-name>
      ```
    - **View all contexts**:
      ```sh
      kubectl config get-contexts
      ```

4. **Namespace Management**:
    - **Get all namespaces**:
      ```sh
      kubectl get namespaces
      ```
    - **Create a namespace**:
      ```sh
      kubectl create namespace <namespace-name>
      ```
    - **Set default namespace**:
      ```sh
      kubectl config set-context --current --namespace=<namespace-name>
      ```

#### Useful Tips

- **Autocomplete**: Enable kubectl command autocompletion.
  ```sh
  source <(kubectl completion bash)  # for Bash
  source <(kubectl completion zsh)   # for Zsh
  ```

- **Dry Run**: Test commands without making changes.
  ```sh
  kubectl apply -f <file.yaml> --dry-run=client
  ```

- **Context Switching**: Quickly switch between clusters.
  ```sh
  kubectl config use-context <context-name>
  ```

- **Label Filtering**: Get resources based on labels.
  ```sh
  kubectl get pods -l <label-key>=<label-value>
  ```

By using this study sheet, new starters can efficiently navigate Kubernetes command line operations and perform essential tasks with confidence.
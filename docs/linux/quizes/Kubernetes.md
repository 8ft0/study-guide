**Question:**

You are tasked with managing Kubernetes clusters using command line tools. Based on your knowledge of Kubernetes command line syntax, answer the following questions:

### Q1: Which command is used to display the current context and cluster information?

A. `kubectl status`

B. `kubectl get context`

C. `kubectl cluster-info`

D. `kubectl show`

### Q2: How would you create a deployment in Kubernetes using a configuration file named `deployment.yaml`?

A. `kubectl apply -f deployment.yaml`

B. `kubectl create -f deployment.yaml`

C. `kubectl deploy -f deployment.yaml`

D. `kubectl start -f deployment.yaml`

### Q3: Which command would you use to list all the pods in the `default` namespace?

A. `kubectl get pods --namespace default`

B. `kubectl get pods -n default`

C. `kubectl get pods`

D. Both A and B

### Q4: How can you scale a deployment named `nginx-deployment` to 5 replicas?

A. `kubectl scale deployment nginx-deployment --replicas=5`

B. `kubectl scale --replicas=5 deployment/nginx-deployment`

C. `kubectl set replicas=5 deployment nginx-deployment`

D. Both A and B

### Q5: Which command is used to delete a service named `my-service` in Kubernetes?

A. `kubectl delete svc my-service`

B. `kubectl remove svc my-service`

C. `kubectl destroy svc my-service`

D. `kubectl delete service my-service`

---

### Answers:

**Q1: Which command is used to display the current context and cluster information?**

- **Answer: C. `kubectl cluster-info`**

- Explanation: The `kubectl cluster-info` command displays information about the current Kubernetes cluster.

**Q2: How would you create a deployment in Kubernetes using a configuration file named `deployment.yaml`?**

- **Answer: A. `kubectl apply -f deployment.yaml`**

- Explanation: The `kubectl apply -f deployment.yaml` command creates or updates resources defined in the `deployment.yaml` file.

**Q3: Which command would you use to list all the pods in the `default` namespace?**

- **Answer: D. Both A and B**

- Explanation: Both `kubectl get pods --namespace default` and `kubectl get pods -n default` can be used to list all the pods in the `default` namespace.

**Q4: How can you scale a deployment named `nginx-deployment` to 5 replicas?**

- **Answer: D. Both A and B**

- Explanation: Both `kubectl scale deployment nginx-deployment --replicas=5` and `kubectl scale --replicas=5 deployment/nginx-deployment` can be used to scale the deployment to 5 replicas.

**Q5: Which command is used to delete a service named `my-service` in Kubernetes?**

- **Answer: D. `kubectl delete service my-service`**

- Explanation: The `kubectl delete service my-service` command deletes the specified service from the Kubernetes cluster.

---


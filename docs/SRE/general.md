# Questions #1

### 1. Difference between VM and Container

- **Virtual Machines (VMs)**: VMs run on physical hardware via a hypervisor. Each VM includes a full copy of an operating system, the application, necessary binaries, and libraries - taking up tens of GBs. VMs can run multiple operating system instances above the virtual hardware layer. They are isolated from the host system and each other, providing complete process and file system isolation.

- **Containers**: Containers share the host system’s kernel but operate in isolated user spaces. They contain only the application and its dependencies. They do not bundle a full OS but include libraries, binaries, etc., required to run the desired software. Containers are more lightweight and use fewer resources than VMs because they leverage the host system’s kernel.

### 2. How are layers created in Docker images?

In Docker, every image begins from a base image, and layers are added on top. Each layer represents an instruction in the image’s Dockerfile. For example:
- `FROM ubuntu:18.04` — the base layer
- `RUN apt-get update && apt-get install -y git` — creates a new layer
- `COPY . /app` — adds the contents of the current directory as a new layer
- `RUN make /app` — builds the application

Each layer is only stored once and is reused across images, which saves space on disk and speeds up processing time. Layers are cached and are read-only.

### 3. Describe Kubernetes Components

- **API Server (kube-apiserver)**: Acts as the front-end to the control plane. It exposes the Kubernetes API and is the only component that communicates with the cluster’s etcd storage.
- **Scheduler (kube-scheduler)**: Responsible for distributing work or containers across multiple nodes. It looks for newly created pods that have no node assigned and selects a node for them to run on.
- **Controller Manager (kube-controller-manager)**: Runs controller processes. These background threads handle routine tasks in the cluster. For example, the Replication Controller ensures that the number of replicas for each pod matches the user-defined number.
- **etcd**: Consistent and highly-available key value store used as Kubernetes’ backing store for all cluster data.
- **Kubelet**: An agent running on each node in the cluster. It makes sure containers are running in a Pod.
- **Kube-proxy**: Manages network communication between Pods and external network.

### 4. Process of Creating a New Pod in Kubernetes

1. **API Request**: A request is sent to the API Server to create a new Pod. This request includes the Pod specification.
2. **Scheduling**: The API Server stores the Pod specification in etcd. The Scheduler watches for new Pods with no assigned node, selects a suitable node, and updates the Pod's information in etcd.
3. **Starting the Pod**: Kubelet on the chosen node watches etcd for Pods that are scheduled to it. When it finds a new Pod, it instructs the container runtime (e.g., Docker) to pull the required image and start the container.
4. **Proxying and Load Balancing**: Kube-proxy configures the node's network so that the Pod can communicate with other Pods across the network.

### 5. Structure of the URL 

- **URL Structure**: A URL typically consists of the following:
  - Protocol (e.g., HTTP, HTTPS)
  - Hostname or IP Address
  - Port (optional)
  - Path to a specific resource
  - Query string (optional)
  - Fragment (optional)

### 6. OSI Model

- **OSI Model**: The Open Systems Interconnection (OSI) model is a conceptual framework used to understand network interactions in seven layers:
  1. Physical
  2. Data Link
  3. Network
  4. Transport
  5. Session
  6. Presentation
  7. Application

### 7. TCP Three-Way Handshake and Four-Way Termination

- **Three-Way Handshake**:
  1. Client sends SYN (synchronize) to server.
  2. Server responds with SYN-ACK (synchronize-acknowledge).
  3. Client sends ACK (acknowledge).

- **Four-Way Termination**:
  1. Client sends a FIN (finish) signal.
  2. Server acknowledges with ACK.
  3. Server sends a FIN.
  4. Client sends ACK to acknowledge.

### 8. What are Latency and Throughput?

- **Latency**: The time it takes for a packet to travel from source to destination. It impacts how quickly a system can respond to input.
- **Throughput**: The amount of data that can be processed by a system in a given amount of time. It affects the amount of work a system can handle.

### 9. What is SRE?

**Site Reliability Engineering (SRE)** is a discipline that incorporates aspects of software engineering and applies them to infrastructure and operations problems. The goal is to create scalable and highly reliable software systems. SRE role involves tasks such as automation, monitoring, and designing highly reliable systems.
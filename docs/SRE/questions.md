# Questions 

## Virtual Machines and Containers

1. Difference between VM and Container

    - Virtual Machines (VMs VMs run on physical hardware via a hypervisor. Each VM includes a full copy of an operating system, the application, necessary binaries, and libraries - taking up tens of GBs. VMs can run multiple operating system instances above the virtual hardware layer. They are isolated from the host system and each other, providing complete process and file system isolation.

    - Containers Containers share the host system’s kernel but operate in isolated user spaces. They contain only the application and its dependencies. They do not bundle a full OS but include libraries, binaries, etc., required to run the desired software. Containers are more lightweight and use fewer resources than VMs because they leverage the host system’s kernel.


1. What are the security implications of using containers versus VMs?
    - Containers share the host's kernel, making them less isolated than VMs, which can run different operating systems. This makes VMs more secure for applications needing strong isolation.

2. How does container orchestration differ from traditional application deployment?
    - Container orchestration tools like Kubernetes automate the deployment, scaling, and management of containerized applications, offering advantages in microservice architectures compared to traditional deployment which often involves manual scaling and management

---

## Docker and Containerization

2. How are layers created in Docker images?

    - In Docker, every image begins from a base image, and layers are added on top. Each layer represents an instruction in the image’s Dockerfile. For example:

        - `FROM ubuntu:18.04` — the base layer
        - `RUN apt-get update && apt-get install -y git` — creates a new layer
        - `COPY . /app` — adds the contents of the current directory as a new layer
        - `RUN make /app` — builds the application

    - Each layer is only stored once and is reused across images, which saves space on disk and speeds up processing time. Layers are cached and are read-only.

3. What is Docker Swarm and how does it compare to Kubernetes?
    - Docker Swarm is Docker's native clustering and scheduling tool, which is simpler and integrated directly into the Docker ecosystem. Kubernetes is more complex but provides a more powerful and flexible feature set for managing containers at scale.

4. How can you optimize Docker images to reduce their size and build time?
    - To optimize Docker images, use smaller base images, minimize layer count by combining commands, remove unnecessary files, and use multi-stage builds to reduce final image size.

---

## Kubernetes

1. Describe Kubernetes Components

    - **API Server (kube-apiserver)**: Acts as the front-end to the control plane. It exposes the Kubernetes API and is the only component that communicates with the cluster’s etcd storage.
    - **Scheduler (kube-scheduler)**: Responsible for distributing work or containers across multiple nodes. It looks for newly created pods that have no node assigned and selects a node for them to run on.
    - **Controller Manager (kube-controller-manager)**: Runs controller processes. These background threads handle routine tasks in the cluster. For example, the Replication Controller ensures that the number of replicas for each pod matches the user-defined number.
    - **etcd**: Consistent and highly-available key value store used as Kubernetes’ backing store for all cluster data.
    - **Kubelet**: An agent running on each node in the cluster. It makes sure containers are running in a Pod.
    - **Kube-proxy**: Manages network communication between Pods and external network.

4. Process of Creating a New Pod in Kubernetes

    1. **API Request**: A request is sent to the API Server to create a new Pod. This request includes the Pod specification.
    2. **Scheduling**: The API Server stores the Pod specification in etcd. The Scheduler watches for new Pods with no assigned node, selects a suitable node, and updates the Pod's information in etcd.
    3. **Starting the Pod**: Kubelet on the chosen node watches etcd for Pods that are scheduled to it. When it finds a new Pod, it instructs the container runtime (e.g., Docker) to pull the required image and start the container.
    4. **Proxying and Load Balancing**: Kube-proxy configures the node's network so that the Pod can communicate with other Pods across the network.


5. Explain the role and functionality of Custom Resource Definitions (CRDs) in Kubernetes.
    - CRDs allow you to define new, custom resources in Kubernetes that act like native Kubernetes objects, extending its functionality

6. How does Kubernetes handle service discovery and load balancing?
    - Kubernetes uses services to abstract the access to pods, providing a stable IP address and DNS name. Load balancing is handled at the service level, distributing network traffic to available pods.

---

## Networking
7. What are the key differences between TCP and UDP protocols?
    - TCP is connection-oriented, provides reliable delivery, and maintains order of messages. UDP is connectionless, faster, and used where speed is preferable to reliability, such as streaming.

8. Explain the concept of network segmentation and its benefits.
    - It divides a network into smaller parts to improve performance and security. Segmentation helps contain network problems and minimize the impact of breaches.



### URL and Web Technologies


5. **URL Structure**: A URL typically consists of the following:

    - Protocol (e.g., HTTP, HTTPS)
    - Hostname or IP Address
    - Port (optional)
    - Path to a specific resource
    - Query string (optional)
    - Fragment (optional)

9. How do HTTP cookies work and what are their security implications?
    - Cookies are data files stored on the client's computer by web browsers to remember stateful information (e.g., items added in the shopping cart) or the user's browsing activity. Security implications include privacy concerns and potential misuse for tracking.

10. What is the difference between HTTP/1.1 and HTTP/2?
    - HTTP/2 is more efficient, allowing multiple requests and responses between client and server over a single connection simultaneously, improving web page load times compared to HTTP/1.1's one request per connection limit.

### OSI Model Deep Dive

1. **OSI Model**: The Open Systems Interconnection (OSI) model is a conceptual framework used to understand network interactions in seven layers:

    1. Physical
    2. Data Link
    3. Network
    4. Transport
    5. Session
    6. Presentation
    7. Application

11. How do different layers of the OSI model interact during a web browsing session?
    - When browsing, data travels from the application layer down to the physical layer on the sender’s side, across the network, and then up from the physical layer to the application layer on the receiver’s side.

12. What are some common security protocols at the Presentation and Application layers?
    - Common protocols include TLS/SSL for secure communications over the internet, and MIME for formatting messages the application layer sends and receives.

### TCP/IP Protocols

7. TCP Three-Way Handshake and Four-Way Termination

    - **Three-Way Handshake**:
        1. Client sends SYN (synchronize) to server.
        2. Server responds with SYN-ACK (synchronize-acknowledge).
        3. Client sends ACK (acknowledge).

    - **Four-Way Termination**:
        1. Client sends a FIN (finish) signal.
        2. Server acknowledges with ACK.
        3. Server sends a FIN.
        4. Client sends ACK to acknowledge.

13. What is the purpose of the ARP protocol and how does it work?
    - The Address Resolution Protocol (ARP) resolves IP addresses to MAC addresses, allowing devices to communicate within a local network segment.

14. Describe how SSL/TLS provides security over the transport layer.
    - SSL/TLS encrypts data at the transport layer, providing secure transmission of information across potentially insecure networks like the internet.

---

## Performance Metrics

8. What are Latency and Throughput?

    - **Latency**: The time it takes for a packet to travel from source to destination. It impacts how quickly a system can respond to input.
    - **Throughput**: The amount of data that can be processed by a system in a given amount of time. It affects the amount of work a system can handle.

15. How can you measure and improve the latency of a web service?
    - Latency can be measured using tools like Ping or Traceroute. Improvements can be made by optimizing server response times, increasing bandwidth, and using content delivery networks (CDNs).

16. What are some tools and techniques for performance benchmarking in a cloud environment?
    - Tools such as Apache JMeter, LoadRunner, or cloud-specific tools like AWS CloudWatch can be used to simulate user requests and measure performance metrics.

---

## Site Reliability Engineering

1. What is SRE?

    - **Site Reliability Engineering (SRE)** is a discipline that incorporates aspects of software engineering and applies them to infrastructure and operations problems. The goal is to create scalable and highly reliable software systems. SRE role involves tasks such as automation, monitoring, and designing highly reliable systems.

17. How does SRE differ from traditional IT operations?
    - SRE focuses on automating operations tasks and maintaining system reliability through software engineering, whereas traditional IT operations may focus more on manual setup, monitoring, and intervention.

18. What are the key metrics that SREs typically monitor, and why?
    - SREs monitor metrics like service uptime, error rates, traffic, latency, and saturation to ensure that the system meets its defined service level objectives (SLOs) and to predict and prevent future problems.

---
These questions can help deepen understanding of various aspects of IT infrastructure, networking, and system reliability, making them suitable for educational, interview, or professional discussion settings.


### Kubernetes on Bare Metal Cheat Sheet

**Purpose**: To provide a quick reference for setting up and managing Kubernetes on bare metal servers.

---

#### Prerequisites

1. **Hardware Requirements**:
    - At least two machines (one master and one or more worker nodes).
    - Minimum resources per node: 2 CPUs, 2 GB RAM, and 20 GB disk space.

2. **Software Requirements**:
    - Ubuntu, CentOS, or another compatible Linux distribution.
    - Docker installed on all nodes.
    - Kubernetes components: `kubeadm`, `kubelet`, and `kubectl`.

3. **Network Requirements**:
    - Unique hostname, MAC address, and product_uuid for each node.
    - Disable swap on all nodes:
      ```sh
      sudo swapoff -a
      sudo sed -i '/ swap / s/^/#/' /etc/fstab
      ```

4. **IP Tables Configuration**:
    - Ensure `net.bridge.bridge-nf-call-iptables` is set to 1:
      ```sh
      sudo modprobe br_netfilter
      echo '1' | sudo tee /proc/sys/net/bridge/bridge-nf-call-iptables
      ```

#### Installing Docker

1. **Install Docker**:
    - **Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install -y docker.io
      sudo systemctl start docker
      sudo systemctl enable docker
      ```
    - **CentOS**:
      ```sh
      sudo yum install -y yum-utils
      sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      sudo yum install -y docker-ce docker-ce-cli containerd.io
      sudo systemctl start docker
      sudo systemctl enable docker
      ```

#### Installing Kubernetes Components

1. **Add Kubernetes Repository**:
    - **Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install -y apt-transport-https ca-certificates curl
      sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      sudo add-apt-repository "deb https://apt.kubernetes.io/ kubernetes-xenial main"
      ```
    - **CentOS**:
      ```sh
      cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
      [kubernetes]
      name=Kubernetes
      baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
      enabled=1
      gpgcheck=1
      repo_gpgcheck=1
      gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
      EOF
      sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
      ```

2. **Install Kubernetes Components**:
    - **Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install -y kubelet kubeadm kubectl
      sudo systemctl enable kubelet
      sudo systemctl start kubelet
      ```
    - **CentOS**:
      ```sh
      sudo yum install -y kubelet kubeadm kubectl
      sudo systemctl enable kubelet
      sudo systemctl start kubelet
      ```

#### Setting Up the Kubernetes Cluster

1. **Initialize the Master Node**:
    - On the master node:
      ```sh
      sudo kubeadm init --pod-network-cidr=10.244.0.0/16
      ```
    - Set up `kubectl` for the regular user:
      ```sh
      mkdir -p $HOME/.kube
      sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
      sudo chown $(id -u):$(id -g) $HOME/.kube/config
      ```

2. **Install a Pod Network Add-On**:
    - **Flannel**:
      ```sh
      kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
      ```
    - **Calico**:
      ```sh
      kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
      ```

3. **Join Worker Nodes to the Cluster**:
    - On each worker node, run the join command provided by the `kubeadm init` output:
      ```sh
      sudo kubeadm join <master-ip>:<master-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
      ```

4. **Verify the Cluster**:
    - Check the status of the nodes:
      ```sh
      kubectl get nodes
      ```

#### Managing the Cluster

1. **Deploy Applications**:
    - Create a deployment:
      ```sh
      kubectl create deployment nginx --image=nginx
      ```
    - Expose the deployment as a service:
      ```sh
      kubectl expose deployment nginx --port=80 --type=NodePort
      ```

2. **Scaling Applications**:
    - Scale the deployment:
      ```sh
      kubectl scale deployment nginx --replicas=3
      ```

3. **Updating Applications**:
    - Update the deployment with a new image:
      ```sh
      kubectl set image deployment/nginx nginx=nginx:latest
      ```

4. **Managing Nodes**:
    - Drain a node for maintenance:
      ```sh
      kubectl drain <node-name> --ignore-daemonsets
      ```
    - Mark a node as schedulable again:
      ```sh
      kubectl uncordon <node-name>
      ```

5. **Upgrading the Cluster**:
    - Upgrade `kubeadm`:
      ```sh
      sudo apt update && sudo apt install -y kubeadm=1.x.x-00
      ```
    - Upgrade the master node:
      ```sh
      sudo kubeadm upgrade plan
      sudo kubeadm upgrade apply v1.x.x
      ```
    - Upgrade `kubelet` and `kubectl`:
      ```sh
      sudo apt install -y kubelet=1.x.x-00 kubectl=1.x.x-00
      sudo systemctl restart kubelet
      ```

By using this cheat sheet, new starters can efficiently set up and manage a Kubernetes cluster on bare metal servers, ensuring proper configuration and maintenance of the cluster.
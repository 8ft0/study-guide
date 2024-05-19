### Docker Configuration Cheat Sheet

**Purpose**: To provide a quick reference for configuring Docker on a Linux system.

---

#### Basic Docker Configuration

1. **Docker Installation**:
   - **Debian/Ubuntu**:
     ```sh
     sudo apt update
     sudo apt install -y docker.io
     sudo systemctl start docker
     sudo systemctl enable docker
     ```
   - **Red Hat/CentOS**:
     ```sh
     sudo yum install -y yum-utils
     sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
     sudo yum install -y docker-ce docker-ce-cli containerd.io
     sudo systemctl start docker
     sudo systemctl enable docker
     ```

2. **Add User to Docker Group**:
   ```sh
   sudo usermod -aG docker <username>
   ```
   - Apply changes:
     ```sh
     newgrp docker
     ```

#### Docker Daemon Configuration

1. **Edit Docker Daemon Configuration**:
   - Configuration file: `/etc/docker/daemon.json`
   - Open the configuration file:
     ```sh
     sudo nano /etc/docker/daemon.json
     ```
   - Example configuration:
     ```json
     {
       "data-root": "/var/lib/docker",
       "log-level": "warn",
       "storage-driver": "overlay2",
       "insecure-registries" : ["myregistrydomain.com:5000"],
       "registry-mirrors": ["https://registry-mirror.example.com"],
       "dns": ["8.8.8.8", "8.8.4.4"]
     }
     ```

2. **Restart Docker to Apply Changes**:
   ```sh
   sudo systemctl restart docker
   ```

#### Network Configuration

1. **Configure Docker Networking**:
   - Default bridge network configuration file: `/etc/docker/daemon.json`
   - Example to configure default bridge IP range:
     ```json
     {
       "bip": "192.168.1.5/24"
     }
     ```

2. **Custom Docker Network**:
   - Create a new bridge network:
     ```sh
     docker network create --driver bridge my_bridge
     ```
   - Assign a specific subnet to the network:
     ```sh
     docker network create --subnet=192.168.1.0/24 my_custom_network
     ```

#### Docker Storage Configuration

1. **Configure Docker Storage Driver**:
   - Supported storage drivers: `overlay2`, `aufs`, `devicemapper`, `btrfs`, `zfs`
   - Set storage driver in `/etc/docker/daemon.json`:
     ```json
     {
       "storage-driver": "overlay2"
     }
     ```
   - Restart Docker to apply changes:
     ```sh
     sudo systemctl restart docker
     ```

2. **Changing Docker Data Root**:
   - Change data root directory in `/etc/docker/daemon.json`:
     ```json
     {
       "data-root": "/mnt/docker-data"
     }
     ```
   - Restart Docker to apply changes:
     ```sh
     sudo systemctl restart docker
     ```

#### Docker Logging Configuration

1. **Configure Docker Logging Driver**:
   - Supported logging drivers: `json-file`, `syslog`, `journald`, `gelf`, `fluentd`, `awslogs`, `splunk`, `etwlogs`
   - Set logging driver in `/etc/docker/daemon.json`:
     ```json
     {
       "log-driver": "json-file",
       "log-opts": {
         "max-size": "10m",
         "max-file": "3"
       }
     }
     ```
   - Restart Docker to apply changes:
     ```sh
     sudo systemctl restart docker
     ```

#### Docker Registry Configuration

1. **Configure Insecure Registries**:
   - Add insecure registries in `/etc/docker/daemon.json`:
     ```json
     {
       "insecure-registries": ["myregistrydomain.com:5000"]
     }
     ```
   - Restart Docker to apply changes:
     ```sh
     sudo systemctl restart docker
     ```

2. **Configure Registry Mirrors**:
   - Add registry mirrors in `/etc/docker/daemon.json`:
     ```json
     {
       "registry-mirrors": ["https://registry-mirror.example.com"]
     }
     ```
   - Restart Docker to apply changes:
     ```sh
     sudo systemctl restart docker
     ```

#### Docker Swarm Configuration

1. **Initialize Docker Swarm**:
   ```sh
   docker swarm init --advertise-addr <manager-ip>
   ```

2. **Add a Node to Swarm**:
   - Get the join token from the manager node:
     ```sh
     docker swarm join-token worker
     ```
   - Use the token to join the node:
     ```sh
     docker swarm join --token <token> <manager-ip>:2377
     ```

3. **Deploy a Stack**:
   - Create a `docker-compose.yml` file with the stack configuration.
   - Deploy the stack:
     ```sh
     docker stack deploy -c docker-compose.yml <stack-name>
     ```

By using this cheat sheet, new starters can effectively configure Docker on a Linux system, ensuring proper setup and management of Docker environments.
### Docker Command Line Syntax and Configuration Study Sheet

**Purpose**: To provide a quick reference for using Docker command line tools and configuring Docker on a Linux system.

---

#### Basic Docker Commands

1. **Check Docker Version**:
      ```sh
      docker --version
      ```

2. **Run a Docker Container**:
      ```sh
      docker run <image-name>
      ```
      - Run in detached mode:
      ```sh
      docker run -d <image-name>
      ```
      - Run with a specific name:
      ```sh
      docker run --name <container-name> <image-name>
      ```
      - Run and map ports:
      ```sh
      docker run -p <host-port>:<container-port> <image-name>
      ```
      - Run and mount volumes:
      ```sh
      docker run -v <host-path>:<container-path> <image-name>
      ```

3. **List Docker Containers**:
      - Running containers:
      ```sh
      docker ps
      ```
      - All containers:
      ```sh
      docker ps -a
      ```

4. **Stop, Start, and Restart Containers**:
      - Stop a container:
      ```sh
      docker stop <container-id>
      ```
      - Start a container:
      ```sh
      docker start <container-id>
      ```
      - Restart a container:
      ```sh
      docker restart <container-id>
      ```

5. **Remove Containers**:
      - Remove a container:
      ```sh
      docker rm <container-id>
      ```
      - Remove all stopped containers:
      ```sh
      docker container prune
      ```

6. **View Container Logs**:
      ```sh
      docker logs <container-id>
      ```

7. **Execute a Command in a Running Container**:
      ```sh
      docker exec -it <container-id> <command>
      ```
      - Start an interactive shell:
      ```sh
      docker exec -it <container-id> /bin/bash
      ```

#### Docker Images

1. **List Docker Images**:
      ```sh
      docker images
      ```

2. **Pull an Image from Docker Hub**:
      ```sh
      docker pull <image-name>
      ```

3. **Remove an Image**:
      ```sh
      docker rmi <image-id>
      ```

4. **Build an Image from a Dockerfile**:
      ```sh
      docker build -t <image-name> <path-to-dockerfile>
      ```

#### Docker Volumes

1. **Create a Docker Volume**:
      ```sh
      docker volume create <volume-name>
      ```

2. **List Docker Volumes**:
      ```sh
      docker volume ls
      ```

3. **Remove a Docker Volume**:
      ```sh
      docker volume rm <volume-name>
      ```

4. **Inspect a Docker Volume**:
      ```sh
      docker volume inspect <volume-name>
      ```

#### Docker Networks

1. **List Docker Networks**:
      ```sh
      docker network ls
      ```

2. **Create a Docker Network**:
      ```sh
      docker network create <network-name>
      ```

3. **Connect a Container to a Network**:
      ```sh
      docker network connect <network-name> <container-id>
      ```

4. **Disconnect a Container from a Network**:
      ```sh
      docker network disconnect <network-name> <container-id>
      ```

5. **Inspect a Docker Network**:
      ```sh
      docker network inspect <network-name>
      ```

#### Docker Compose

1. **Start Services Defined in `docker-compose.yml`**:
      ```sh
      docker-compose up
      ```
      - Start in detached mode:
      ```sh
      docker-compose up -d
      ```

2. **Stop Services**:
      ```sh
      docker-compose down
      ```

3. **List Containers Managed by Docker Compose**:
      ```sh
      docker-compose ps
      ```

4. **Build or Rebuild Services**:
      ```sh
      docker-compose build
      ```

5. **View Logs for Services**:
      ```sh
      docker-compose logs
      ```

#### Docker Configuration

1. **Configure Docker Daemon**:
      - Edit the Docker daemon configuration file:
      ```sh
      sudo nano /etc/docker/daemon.json
      ```
      - Example configuration:
      ```json
      {
         "data-root": "/custom/path/to/docker",
         "log-level": "warn",
         "storage-driver": "overlay2"
      }
      ```
      - Restart Docker to apply changes:
      ```sh
      sudo systemctl restart docker
      ```

2. **Enable and Start Docker Service**:
      ```sh
      sudo systemctl enable docker
      sudo systemctl start docker
      ```

3. **Check Docker Service Status**:
      ```sh
      sudo systemctl status docker
      ```

#### Common Docker Troubleshooting

1. **Check Docker Logs**:
   ```sh
   sudo journalctl -u docker
   ```

2. **Restart Docker Service**:
   ```sh
   sudo systemctl restart docker
   ```

3. **Check Container Logs**:
   ```sh
   docker logs <container-id>
   ```

4. **Remove Dangling Images**:
   ```sh
   docker image prune
   ```

By using this study sheet, new starters can efficiently manage Docker containers, images, volumes, networks, and configurations, ensuring proper use and maintenance of Docker environments.
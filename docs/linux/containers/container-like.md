### Container-like Features on Linux Without Using Docker

**Purpose**: To provide a quick reference for using container-like features on Linux without relying on Docker.

---

#### Overview

Linux offers several tools and technologies that provide container-like features, allowing for application isolation, resource control, and process management without using Docker. These tools include LXC/LXD, systemd-nspawn, chroot, and namespaces with cgroups.

#### LXC (Linux Containers)

1. **Install LXC**:
    - **Debian/Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install lxc
      ```
    - **Red Hat/CentOS**:
      ```sh
      sudo yum install epel-release
      sudo yum install lxc
      ```

2. **Create and Start a Container**:
    ```sh
    sudo lxc-create -t download -n mycontainer -- -d ubuntu -r focal -a amd64
    sudo lxc-start -n mycontainer
    ```

3. **Attach to a Running Container**:
    ```sh
    sudo lxc-attach -n mycontainer
    ```

4. **List Containers**:
    ```sh
    sudo lxc-ls -f
    ```

5. **Stop and Destroy a Container**:
    ```sh
    sudo lxc-stop -n mycontainer
    sudo lxc-destroy -n mycontainer
    ```

#### LXD (Linux Container Daemon)

1. **Install LXD**:
    - **Debian/Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install lxd
      sudo lxd init
      ```

2. **Launch and Manage Containers**:
    - Launch a container:
      ```sh
      lxc launch ubuntu:20.04 mycontainer
      ```
    - List containers:
      ```sh
      lxc list
      ```
    - Execute a command in a container:
      ```sh
      lxc exec mycontainer -- /bin/bash
      ```
    - Stop and delete a container:
      ```sh
      lxc stop mycontainer
      lxc delete mycontainer
      ```

#### Systemd-nspawn

1. **Install Systemd-nspawn**:
    - **Debian/Ubuntu**:
      ```sh
      sudo apt update
      sudo apt install systemd-container
      ```
    - **Red Hat/CentOS**:
      ```sh
      sudo yum install systemd-container
      ```

2. **Create and Start a Container**:
    - Create a directory for the container's root filesystem:
      ```sh
      mkdir -p /var/lib/machines/mycontainer
      ```
    - Bootstrap a minimal Linux system into this directory (example with `debootstrap` for Debian/Ubuntu):
      ```sh
      sudo debootstrap --arch=amd64 focal /var/lib/machines/mycontainer http://archive.ubuntu.com/ubuntu/
      ```
    - Start the container:
      ```sh
      sudo systemd-nspawn -b -D /var/lib/machines/mycontainer
      ```

3. **Manage Containers**:
    - List running containers:
      ```sh
      machinectl list
      ```
    - Stop a container:
      ```sh
      machinectl poweroff mycontainer
      ```
    - Enter a running container:
      ```sh
      machinectl shell mycontainer
      ```

#### Chroot

1. **Create a Chroot Environment**:
    - Create a directory for the chroot environment:
      ```sh
      sudo mkdir -p /mychroot
      ```
    - Bootstrap a minimal Linux system into this directory (example with `debootstrap` for Debian/Ubuntu):
      ```sh
      sudo debootstrap --arch=amd64 focal /mychroot http://archive.ubuntu.com/ubuntu/
      ```

2. **Enter the Chroot Environment**:
    ```sh
    sudo chroot /mychroot /bin/bash
    ```

3. **Exit the Chroot Environment**:
    ```sh
    exit
    ```

#### Namespaces and Cgroups

1. **Using `unshare` to Create Isolated Environments**:
    - **Install `util-linux`** (if not already installed):
      ```sh
      sudo apt update
      sudo apt install util-linux
      ```
    - Create a new namespace for process isolation:
      ```sh
      sudo unshare --fork --pid --mount-proc /bin/bash
      ```

2. **Using Cgroups for Resource Limitation**:
    - **Install `cgroup-tools`** (if not already installed):
      ```sh
      sudo apt update
      sudo apt install cgroup-tools
      ```
    - Create a new cgroup and limit CPU usage:
      ```sh
      sudo cgcreate -g cpu:/mycgroup
      sudo cgset -r cpu.shares=512 mycgroup
      sudo cgexec -g cpu:/mycgroup /bin/bash
      ```

#### Advantages and Disadvantages

**Advantages**:

  - **Lightweight**: No need to install Docker; uses existing Linux features.
  - **Flexibility**: Fine-grained control over isolation and resource management.
  - **Compatibility**: Works on systems where Docker might not be available or suitable.

**Disadvantages**:

  - **Complexity**: Requires more manual setup and configuration compared to Docker.
  - **Ecosystem**: Lack of a unified toolset and ecosystem that Docker provides.
  - **Ease of Use**: Higher learning curve and less straightforward usage compared to Docker.

By using these tools and techniques, new starters can achieve container-like functionality on Linux systems without relying on Docker, providing flexibility and control over their environments.
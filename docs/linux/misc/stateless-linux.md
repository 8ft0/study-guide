### Stateless Linux Systems Cheat Sheet

**Purpose**: To provide a quick reference for understanding and managing stateless Linux systems, where system state is not preserved across reboots.

---

#### What is a Stateless Linux System?

- **Definition**: A stateless Linux system does not retain any changes made to the system state after a reboot. The system always starts with a predefined state.
- **Use Cases**: Ideal for kiosks, public computers, embedded systems, and environments where consistency and security are critical.

#### Key Concepts

1. **Immutable Root Filesystem**:
    - The root filesystem is read-only, ensuring that no changes can be made to the core system files.
    - Any changes are made in a temporary overlay that is discarded on reboot.

2. **Configuration Management**:
    - System configuration is managed via version-controlled files or central configuration management systems.
    - Tools like Ansible, Puppet, or Chef can be used to ensure consistent configuration.

3. **Data Persistence**:
    - User data and logs can be stored in separate, persistent storage locations if needed.
    - Persistent storage is often mounted on separate partitions or external storage devices.

#### Setting Up a Stateless Linux System

1. **Create a Read-Only Root Filesystem**:
    - **Using OverlayFS**:
        - OverlayFS allows creating a read-only base layer with a writable upper layer.
        - Example fstab entry:
          ```sh
          none / overlay defaults,lowerdir=/ro-root,upperdir=/rw-root,workdir=/work 0 0
          ```

2. **System Configuration Management**:
    - Use configuration management tools to automate system setup.
    - Example with Ansible:
      ```yaml
      - name: Ensure stateless configuration
        hosts: all
        tasks:
          - name: Copy configuration files
            copy:
              src: /path/to/config/
              dest: /etc/
          - name: Install necessary packages
            package:
              name:
                - package1
                - package2
              state: present
      ```

3. **Persistent Data Storage**:
    - Mount persistent storage for user data and logs.
    - Example fstab entries:
      ```sh
      /dev/sdb1 /var/log ext4 defaults 0 0
      /dev/sdc1 /home ext4 defaults 0 0
      ```

4. **Network Configuration**:
    - Ensure network settings are applied on each boot using network management tools or scripts.
    - Example network configuration script:
      ```sh
      #!/bin/bash
      ip link set dev eth0 up
      ip addr add 192.168.1.100/24 dev eth0
      ip route add default via 192.168.1.1
      ```

#### Booting a Stateless System

1. **PXE Boot**:
    - Stateless systems can boot over the network using PXE (Preboot Execution Environment).
    - Configure a PXE server to serve the boot images and configuration.
    - Example PXE configuration:
      ```sh
      DEFAULT linux
      LABEL linux
        KERNEL vmlinuz
        APPEND initrd=initrd.img root=/dev/nfs nfsroot=192.168.1.1:/nfs/root rw ip=dhcp
      ```

2. **Live CD/USB**:
    - Use a live CD or USB to boot a stateless system.
    - Create a bootable live image with tools like `mkisofs` or `dd`.
    - Example `dd` command:
      ```sh
      sudo dd if=live-image.iso of=/dev/sdX bs=4M status=progress
      ```

3. **System Reset on Reboot**:
    - Configure the system to reset to the predefined state on reboot.
    - Use a script to clear changes and reset the state:
      ```sh
      #!/bin/bash
      mount -o remount,ro /
      rm -rf /rw-root/*
      reboot
      ```

#### Advantages and Disadvantages

**Advantages**:

  - **Consistency**: Always boots into a known state, reducing configuration drift.
  - **Security**: Changes are not persistent, reducing the risk of persistent malware.
  - **Maintenance**: Simplified management and updates.

**Disadvantages**:

  - **Limited Customization**: Users cannot make permanent changes.
  - **Data Management**: Requires careful planning for data persistence.

By using this cheat sheet, new starters can efficiently understand and set up stateless Linux systems, ensuring proper implementation and management of such environments.
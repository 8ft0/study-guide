### Linux Networking Configuration Cheat Sheet

**Purpose**: To provide a quick reference for configuring and managing network settings on a Linux system.

---

#### Viewing Network Configuration

1. **Display Network Interfaces**:
    ```sh
    ip a
    ```
    - Alternative command:
      ```sh
      ifconfig
      ```

2. **Display Routing Table**:
    ```sh
    ip route
    ```
    - Alternative command:
      ```sh
      route -n
      ```

3. **Display DNS Configuration**:
   ```sh
   cat /etc/resolv.conf
   ```

#### Configuring Network Interfaces

1. **Using `ip` Command**:
    - Assign an IP address:
      ```sh
      sudo ip addr add 192.168.1.100/24 dev eth0
      ```
    - Bring an interface up:
      ```sh
      sudo ip link set dev eth0 up
      ```
    - Bring an interface down:
      ```sh
      sudo ip link set dev eth0 down
      ```

2. **Using `ifconfig` Command**:
    - Assign an IP address:
      ```sh
      sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
      ```
    - Bring an interface up:
      ```sh
      sudo ifconfig eth0 up
      ```
    - Bring an interface down:
      ```sh
      sudo ifconfig eth0 down
      ```

3. **Persistent Network Configuration**:
    - **Debian/Ubuntu**: Edit `/etc/network/interfaces`:
      ```sh
      sudo nano /etc/network/interfaces
      ```
    - Example configuration:
      ```sh
      auto eth0
      iface eth0 inet static
          address 192.168.1.100
          netmask 255.255.255.0
          gateway 192.168.1.1
          dns-nameservers 1.1.1.1 8.8.8.8
      ```

    - **Red Hat/CentOS**: Edit the interface configuration file (e.g., `/etc/sysconfig/network-scripts/ifcfg-eth0`):
      ```sh
      sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0
      ```
    - Example configuration:
      ```sh
      DEVICE=eth0
      BOOTPROTO=static
      ONBOOT=yes
      IPADDR=192.168.1.100
      NETMASK=255.255.255.0
      GATEWAY=192.168.1.1
      DNS1=1.1.1.1
      DNS2=8.8.8.8
      ```

#### Configuring Hostname

1. **View Current Hostname**:
   ```sh
   hostname
   ```

2. **Set Temporary Hostname**:
   ```sh
   sudo hostnamectl set-hostname <new-hostname>
   ```

3. **Edit Hostname Permanently**:
    - **Debian/Ubuntu**: Edit `/etc/hostname`:
      ```sh
      sudo nano /etc/hostname
      ```
    - **Red Hat/CentOS**: Edit `/etc/hostname`:
      ```sh
      sudo nano /etc/hostname
      ```

#### Configuring Static Routes

1. **Add a Static Route**:
   ```sh
   sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
   ```

2. **Delete a Static Route**:
   ```sh
   sudo ip route del 192.168.2.0/24
   ```

3. **Persistent Static Routes**:
    - **Debian/Ubuntu**: Edit `/etc/network/interfaces`:
      ```sh
      sudo nano /etc/network/interfaces
      ```
    - Add static route configuration:
      ```sh
      up ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
      ```

    - **Red Hat/CentOS**: Create a static route file (e.g., `/etc/sysconfig/network-scripts/route-eth0`):
      ```sh
      sudo nano /etc/sysconfig/network-scripts/route-eth0
      ```
    - Add static route configuration:
      ```sh
      192.168.2.0/24 via 192.168.1.1 dev eth0
      ```

#### Configuring Firewall

1. **Using `iptables`**:
    - View current rules:
      ```sh
      sudo iptables -L
      ```
    - Allow incoming SSH connections:
      ```sh
      sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
      ```
    - Save iptables rules (Debian/Ubuntu):
      ```sh
      sudo iptables-save | sudo tee /etc/iptables/rules.v4
      ```
    - Save iptables rules (Red Hat/CentOS):
      ```sh
      sudo service iptables save
      ```

2. **Using `firewalld`**:
    - Start and enable `firewalld`:
      ```sh
      sudo systemctl start firewalld
      sudo systemctl enable firewalld
      ```
    - Allow a service (e.g., SSH):
      ```sh
      sudo firewall-cmd --permanent --add-service=ssh
      sudo firewall-cmd --reload
      ```

3. **Using `ufw` (Uncomplicated Firewall)**:
    - Enable `ufw`:
      ```sh
      sudo ufw enable
      ```
    - Allow SSH connections:
      ```sh
      sudo ufw allow ssh
      ```
    - View status:
      ```sh
      sudo ufw status
      ```

#### Network Troubleshooting

1. **Ping a Host**:
   ```sh
   ping <hostname-or-ip>
   ```

2. **Trace Route to a Host**:
   ```sh
   traceroute <hostname-or-ip>
   ```

3. **Check DNS Resolution**:
   ```sh
   nslookup <hostname>
   ```

4. **Check Open Ports**:
   ```sh
   sudo netstat -tuln
   ```

5. **Test Connectivity with `curl`**:
   ```sh
   curl -I <url>
   ```

By using this cheat sheet, new starters can efficiently configure and manage network settings on a Linux system, ensuring proper connectivity and network performance.
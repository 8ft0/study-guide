### Linux DNS Configuration Cheat Sheet

**Purpose**: To provide a quick reference for configuring DNS settings on a Linux system.

---

#### Checking Current DNS Settings

1. **View Current DNS Servers**:
    ```sh
    cat /etc/resolv.conf
    ```
    - Typical output:
      ```
      nameserver 8.8.8.8
      nameserver 8.8.4.4
      ```

#### Configuring DNS Settings

1. **Editing `/etc/resolv.conf`**:
    - Open the file in a text editor (e.g., `nano` or `vim`):
      ```sh
      sudo nano /etc/resolv.conf
      ```
    - Add or modify nameserver entries:
      ```sh
      nameserver 1.1.1.1
      nameserver 8.8.8.8
      ```

2. **Persistent DNS Configuration**:
    - **NetworkManager**: If your system uses NetworkManager, you should update DNS settings through its configuration to make changes persistent.

    - Open the NetworkManager configuration file:
      ```sh
      sudo nano /etc/NetworkManager/NetworkManager.conf
      ```
    - Add or modify the DNS settings:
      ```sh
      [main]
      dns=default
      ```
    - Restart NetworkManager to apply changes:
      ```sh
      sudo systemctl restart NetworkManager
      ```

3. **Using `nmcli` (NetworkManager Command Line Interface)**:
    - List connections:
      ```sh
      nmcli con show
      ```
    - Modify DNS settings for a specific connection:
      ```sh
      nmcli con mod <connection-name> ipv4.dns "1.1.1.1 8.8.8.8"
      nmcli con up <connection-name>
      ```

4. **Systemd-Resolved Configuration**:
    - For systems using `systemd-resolved`, you can configure DNS settings in `/etc/systemd/resolved.conf`:
      ```sh
      sudo nano /etc/systemd/resolved.conf
      ```
    - Update or add DNS settings:
      ```ini
      [Resolve]
      DNS=1.1.1.1 8.8.8.8
      FallbackDNS=8.8.4.4
      ```
    - Restart the `systemd-resolved` service to apply changes:
      ```sh
      sudo systemctl restart systemd-resolved
      ```

5. **Adding DNS Servers in Network Interface Configuration**:
    - If you configure network interfaces directly, you can specify DNS settings in the interface configuration files.
    - **Debian/Ubuntu**: Edit `/etc/network/interfaces`:
      ```sh
      sudo nano /etc/network/interfaces
      ```
    - Add DNS settings for an interface:
      ```sh
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
    - Add DNS settings:
      ```sh
      DNS1=1.1.1.1
      DNS2=8.8.8.8
      ```

#### Testing DNS Configuration

1. **Test DNS Resolution**:
    - Use `nslookup`:
      ```sh
      nslookup example.com
      ```
    - Use `dig`:
      ```sh
      dig example.com
      ```
    - Use `host`:
      ```sh
      host example.com
      ```

2. **Flush DNS Cache** (if applicable):
    - **systemd-resolved**:
      ```sh
      sudo systemd-resolve --flush-caches
      ```
    - **DNSMasq**:
      ```sh
      sudo systemctl restart dnsmasq
      ```

By using this cheat sheet, new starters can efficiently configure and manage DNS settings on a Linux system, ensuring proper network resolution and connectivity.
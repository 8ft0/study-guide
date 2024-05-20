### Security and Access Control Cheat Sheet

**Purpose**: To provide a quick reference for enhancing security and managing access control on a Linux system.

---

#### Basic Security Practices

1. **Regular Updates**:

    - Keep the system updated to protect against vulnerabilities.
      ```sh
      sudo apt update && sudo apt upgrade   # Debian/Ubuntu
      sudo yum update                       # Red Hat/CentOS
      sudo dnf update                       # Fedora
      ```

2. **User Management**:
    - Create a new user:
      ```sh
      sudo adduser <username>
      ```
    - Grant sudo privileges:
      ```sh
      sudo usermod -aG sudo <username>      # Debian/Ubuntu
      sudo usermod -aG wheel <username>     # Red Hat/CentOS
      ```

#### Firewall Configuration

1. **Using UFW (Uncomplicated Firewall)**:
    - Enable UFW:
      ```sh
      sudo ufw enable
      ```
    - Allow specific services:
      ```sh
      sudo ufw allow ssh
      sudo ufw allow http
      sudo ufw allow https
      ```
    - Check UFW status:
      ```sh
      sudo ufw status
      ```

2. **Using iptables**:
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

3. **Using firewalld**:
    - Start and enable firewalld:
      ```sh
      sudo systemctl start firewalld
      sudo systemctl enable firewalld
      ```
    - Allow a service (e.g., SSH):
      ```sh
      sudo firewall-cmd --permanent --add-service=ssh
      sudo firewall-cmd --reload
      ```
    - Check firewalld status:
      ```sh
      sudo firewall-cmd --state
      ```

#### SSH Configuration

1. **Configure SSH Daemon**:
    - Edit SSH configuration:
      ```sh
      sudo nano /etc/ssh/sshd_config
      ```
    - Disable root login:
      ```sh
      PermitRootLogin no
      ```
    - Change the default SSH port:
      ```sh
      Port 2222
      ```
    - Restrict user access:
      ```sh
      AllowUsers <username>
      ```

2. **Restart SSH Service**:
   ```sh
   sudo systemctl restart sshd
   ```

3. **Set Up SSH Key Authentication**:
    - Generate SSH key pair on the client:
      ```sh
      ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
      ```
    - Copy the public key to the server:
      ```sh
      ssh-copy-id <username>@<server-ip>
      ```

#### Intrusion Detection

1. **Install and Configure Fail2Ban**:
    - Install Fail2Ban:
      ```sh
      sudo apt install fail2ban   # Debian/Ubuntu
      sudo yum install fail2ban   # Red Hat/CentOS
      ```
    - Configure Fail2Ban:
      ```sh
      sudo nano /etc/fail2ban/jail.local
      ```
    - Example configuration:
      ```ini
      [sshd]
      enabled = true
      port = 22
      logpath = /var/log/auth.log
      bantime = 600
      maxretry = 3
      ```
    - Start and enable Fail2Ban:
      ```sh
      sudo systemctl start fail2ban
      sudo systemctl enable fail2ban
      ```

2. **Install and Configure AIDE** (Advanced Intrusion Detection Environment):
    - Install AIDE:
      ```sh
      sudo apt install aide   # Debian/Ubuntu
      sudo yum install aide   # Red Hat/CentOS
      ```
    - Initialize AIDE database:
      ```sh
      sudo aide --init
      ```
    - Move the new database to the default location:
      ```sh
      sudo mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
      ```
    - Perform a manual check:
      ```sh
      sudo aide --check
      ```

#### Access Control with SELinux and AppArmor

1. **SELinux**:
    - Check SELinux status:
      ```sh
      sestatus
      ```
    - Change SELinux mode (temporarily):
      ```sh
      sudo setenforce 0   # Permissive mode
      sudo setenforce 1   # Enforcing mode
      ```
    - Configure SELinux mode permanently:
      ```sh
      sudo nano /etc/selinux/config
      ```
      - Change `SELINUX` directive:
        ```sh
        SELINUX=enforcing   # or permissive or disabled
        ```

2. **AppArmor**:
    - Check AppArmor status:
      ```sh
      sudo apparmor_status
      ```
    - Enable or disable a profile:
      ```sh
      sudo aa-enforce /etc/apparmor.d/<profile>
      sudo aa-disable /etc/apparmor.d/<profile>
      ```

#### Data Encryption

1. **Encrypt Partitions with LUKS**:
    - Install cryptsetup:
      ```sh
      sudo apt install cryptsetup   # Debian/Ubuntu
      sudo yum install cryptsetup   # Red Hat/CentOS
      ```
    - Encrypt a partition:
      ```sh
      sudo cryptsetup luksFormat /dev/sdX
      ```
    - Open the encrypted partition:
      ```sh
      sudo cryptsetup luksOpen /dev/sdX my_encrypted_partition
      ```
    - Create a filesystem:
      ```sh
      sudo mkfs.ext4 /dev/mapper/my_encrypted_partition
      ```
    - Mount the encrypted partition:
      ```sh
      sudo mount /dev/mapper/my_encrypted_partition /mnt
      ```

#### Auditing and Logging

1. **Set Up Auditd**:
    - Install auditd:
      ```sh
      sudo apt install auditd   # Debian/Ubuntu
      sudo yum install audit    # Red Hat/CentOS
      ```
    - Start and enable auditd:
      ```sh
      sudo systemctl start auditd
      sudo systemctl enable auditd
      ```
    - Configure audit rules:
      ```sh
      sudo nano /etc/audit/audit.rules
      ```
    - Example rules:
      ```sh
      -w /etc/passwd -p wa -k passwd_changes
      -w /var/log/auth.log -p wa -k auth_logs
      ```

2. **Log Management with rsyslog**:
    - Configure rsyslog:
      ```sh
      sudo nano /etc/rsyslog.conf
      ```
    - Example configuration:
      ```sh
      *.info;mail.none;authpriv.none;cron.none                /var/log/messages
      authpriv.*                                              /var/log/secure
      mail.*                                                  -/var/log/maillog
      cron.*                                                  /var/log/cron
      ```
    - Restart rsyslog:
      ```sh
      sudo systemctl restart rsyslog
      ```

By using this cheat sheet, new starters can effectively secure and manage access control on a Linux system, ensuring proper protection and monitoring of the system.
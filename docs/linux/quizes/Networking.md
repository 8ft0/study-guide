Linux Networking Configuration:

---

**Question:**

You are tasked with configuring network settings on a Linux system. Based on your knowledge of Linux networking configuration files and commands, answer the following questions:

### Q1: Which file is primarily used to configure network interfaces on a Debian-based Linux system?

A. `/etc/sysconfig/network-scripts/ifcfg-eth0`

B. `/etc/network/interfaces`

C. `/etc/netplan/config.yaml`

D. `/etc/sysconfig/network`

### Q2: Which command would you use to display the current network interfaces and their configurations?

A. `ifconfig`

B. `netstat`

C. `ip addr show`

D. `route`

### Q3: How would you restart the networking service on a system using `systemd`?

A. `service network restart`

B. `/etc/init.d/networking restart`

C. `systemctl restart networking`

D. `network restart`

### Q4: What command can be used to view the routing table on a Linux system?

A. `netstat -r`

B. `route`

C. `ip route`

D. `all of the above`

### Q5: To configure a static IP address on a CentOS/RHEL system, which file would you typically modify?

A. `/etc/network/interfaces`

B. `/etc/sysconfig/network-scripts/ifcfg-eth0`

C. `/etc/resolv.conf`

D. `/etc/hostname`

---

### Answers:

**Q1: Which file is primarily used to configure network interfaces on a Debian-based Linux system?**

- **Answer: B. `/etc/network/interfaces`**

- Explanation: On Debian-based systems, the `/etc/network/interfaces` file is used to configure network interfaces.

**Q2: Which command would you use to display the current network interfaces and their configurations?**

- **Answer: C. `ip addr show`**

- Explanation: The `ip addr show` command is used to display network interfaces and their configurations. Although `ifconfig` can also be used, it is deprecated in favour of the `ip` command.

**Q3: How would you restart the networking service on a system using `systemd`?**

- **Answer: C. `systemctl restart networking`**

- Explanation: The `systemctl restart networking` command is used to restart the networking service on systems using `systemd`.

**Q4: What command can be used to view the routing table on a Linux system?**

- **Answer: D. `all of the above`**

- Explanation: The commands `netstat -r`, `route`, and `ip route` can all be used to view the routing table on a Linux system.

**Q5: To configure a static IP address on a CentOS/RHEL system, which file would you typically modify?**

- **Answer: B. `/etc/sysconfig/network-scripts/ifcfg-eth0`**

- Explanation: On CentOS/RHEL systems, network interface configuration is typically done by modifying the appropriate file in the `/etc/sysconfig/network-scripts/` directory, such as `ifcfg-eth0`.

---


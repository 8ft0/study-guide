Linux DNS configuration:

---

**Question:**

You are tasked with configuring DNS on a Linux system. Based on your knowledge of DNS configuration files and commands, answer the following questions:

### Q1: Which file is primarily used to configure the system's DNS resolver?

A. `/etc/hosts`

B. `/etc/nsswitch.conf`

C. `/etc/resolv.conf`

D. `/etc/hostname`

### Q2: In the `/etc/resolv.conf` file, which directive is used to specify the DNS server?

A. `search`

B. `nameserver`

C. `domain`

D. `server`

### Q3: Which command would you use to test DNS resolution for the domain `example.com`?

A. `ping example.com`

B. `dig example.com`

C. `nslookup example.com`

D. `host example.com`

### Q4: In the context of DNS, what does the term "forwarder" refer to?

A. A DNS server that forwards queries to other DNS servers if it cannot resolve them itself.

B. A DNS server that caches DNS queries to speed up resolution.

C. A DNS record that points to another domain name.

D. A DNS server that resolves internal network names.

### Q5: To change the DNS server on a system using NetworkManager, which command would you use?

A. `nmcli dev dns set`

B. `nmcli dev set dns`

C. `nmcli con mod <connection_name> ipv4.dns <dns_server>`

D. `nmcli con set <connection_name> dns <dns_server>`

---

### Answers:

**Q1: Which file is primarily used to configure the system's DNS resolver?**

- **Answer: C. `/etc/resolv.conf`**

- Explanation: The file `/etc/resolv.conf` is used to configure the system's DNS resolver by specifying the DNS servers and search domain.

**Q2: In the `/etc/resolv.conf` file, which directive is used to specify the DNS server?**

- **Answer: B. `nameserver`**

- Explanation: The `nameserver` directive in the `/etc/resolv.conf` file is used to specify the IP address of a DNS server.

**Q3: Which command would you use to test DNS resolution for the domain `example.com`?**

- **Answer: B. `dig example.com`**

- Explanation: The `dig` command is used to perform DNS lookups and can be used to test DNS resolution.

**Q4: In the context of DNS, what does the term "forwarder" refer to?**

- **Answer: A. A DNS server that forwards queries to other DNS servers if it cannot resolve them itself.**

- Explanation: A forwarder is a DNS server that forwards queries to other DNS servers if it cannot resolve them locally.

**Q5: To change the DNS server on a system using NetworkManager, which command would you use?**

- **Answer: C. `nmcli con mod <connection_name> ipv4.dns <dns_server>`**

- Explanation: The command `nmcli con mod <connection_name> ipv4.dns <dns_server>` is used to modify the DNS server settings for a specific network connection managed by NetworkManager.

---


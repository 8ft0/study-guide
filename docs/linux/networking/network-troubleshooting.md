### Networking Troubleshooting Cheat Sheet

**Purpose**: To provide a quick reference for diagnosing and resolving network issues on a Linux system.

---

#### Basic Connectivity Checks

1. **Ping a Host**:
   - Check connectivity to a remote host:
     ```sh
     ping <hostname-or-ip>
     ```
   - Continuous ping:
     ```sh
     ping -c 5 <hostname-or-ip>
     ```

2. **Check Local Network Configuration**:
   - Display all network interfaces and IP addresses:
     ```sh
     ip a
     ```
   - Alternative command:
     ```sh
     ifconfig
     ```

3. **Check Routing Table**:
   - Display current routing table:
     ```sh
     ip route
     ```
   - Alternative command:
     ```sh
     route -n
     ```

4. **Check Default Gateway**:
   - Verify the default gateway setting:
     ```sh
     ip route | grep default
     ```

#### Advanced Diagnostics

1. **Traceroute**:
   - Trace the path to a remote host:
     ```sh
     traceroute <hostname-or-ip>
     ```
   - For systems without `traceroute`:
     ```sh
     sudo apt install traceroute  # Debian/Ubuntu
     sudo yum install traceroute  # Red Hat/CentOS
     ```

2. **DNS Resolution**:
   - Check DNS resolution:
     ```sh
     nslookup <hostname>
     ```
   - Alternative command:
     ```sh
     dig <hostname>
     ```
   - Simple DNS lookup:
     ```sh
     host <hostname>
     ```

3. **Check Open Ports**:
   - List listening ports:
     ```sh
     sudo netstat -tuln
     ```
   - Alternative command:
     ```sh
     sudo ss -tuln
     ```

4. **Check Network Interfaces**:
   - Display interface statistics:
     ```sh
     ip -s link
     ```

5. **Check ARP Table**:
   - Display ARP table entries:
     ```sh
     ip neigh
     ```
   - Alternative command:
     ```sh
     arp -a
     ```

6. **Check Active Connections**:
   - Display all active connections:
     ```sh
     sudo netstat -an
     ```
   - Alternative command:
     ```sh
     sudo ss -an
     ```

#### Packet Analysis

1. **Tcpdump**:
   - Capture packets on a specific interface:
     ```sh
     sudo tcpdump -i <interface>
     ```
   - Capture and save packets to a file:
     ```sh
     sudo tcpdump -i <interface> -w capture.pcap
     ```
   - Capture packets with specific filter:
     ```sh
     sudo tcpdump -i <interface> tcp port 80
     ```

2. **Wireshark**:
   - Install Wireshark:
     ```sh
     sudo apt install wireshark  # Debian/Ubuntu
     sudo yum install wireshark  # Red Hat/CentOS
     ```
   - Use Wireshark GUI to capture and analyze network traffic.

#### Common Networking Tools

1. **Telnet**:
   - Check connectivity to a specific port:
     ```sh
     telnet <hostname> <port>
     ```
   - Install Telnet client:
     ```sh
     sudo apt install telnet  # Debian/Ubuntu
     sudo yum install telnet  # Red Hat/CentOS
     ```

2. **Nmap**:
   - Scan open ports on a host:
     ```sh
     nmap <hostname-or-ip>
     ```
   - Install Nmap:
     ```sh
     sudo apt install nmap  # Debian/Ubuntu
     sudo yum install nmap  # Red Hat/CentOS
     ```

3. **Curl**:
   - Test HTTP/HTTPS connectivity:
     ```sh
     curl -I <url>
     ```

4. **Netcat**:
   - Check if a port is open:
     ```sh
     nc -zv <hostname> <port>
     ```
   - Listen on a port:
     ```sh
     nc -l <port>
     ```

#### Network Configuration Files

1. **/etc/resolv.conf**:
   - DNS server configuration:
     ```sh
     cat /etc/resolv.conf
     ```

2. **/etc/hosts**:
   - Local hostname resolution:
     ```sh
     cat /etc/hosts
     ```

3. **/etc/network/interfaces** (Debian/Ubuntu):
   - Network interface configuration:
     ```sh
     cat /etc/network/interfaces
     ```

4. **/etc/sysconfig/network-scripts/ifcfg-<interface>** (Red Hat/CentOS):
   - Network interface configuration:
     ```sh
     cat /etc/sysconfig/network-scripts/ifcfg-<interface>
     ```

#### Network Service Management

1. **Restart Network Services**:
   - Debian/Ubuntu:
     ```sh
     sudo systemctl restart networking
     ```
   - Red Hat/CentOS:
     ```sh
     sudo systemctl restart network
     ```

2. **Check Network Service Status**:
   ```sh
   sudo systemctl status networking  # Debian/Ubuntu
   sudo systemctl status network     # Red Hat/CentOS
   ```

#### Persistent Network Issues

1. **Check System Logs**:
   - View system logs for network-related messages:
     ```sh
     sudo journalctl -u networking  # Debian/Ubuntu
     sudo journalctl -u network     # Red Hat/CentOS
     ```

2. **Inspect Interface Configuration**:
   - Verify the configuration files for errors or misconfigurations.

3. **Hardware Issues**:
   - Check for hardware problems such as faulty cables, network cards, or switches.

By using this cheat sheet, new starters can efficiently diagnose and resolve network issues on a Linux system, ensuring proper network connectivity and performance.
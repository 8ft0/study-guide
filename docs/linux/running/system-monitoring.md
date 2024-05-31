### Linux System Monitoring Study Sheet

**Purpose**: To provide a quick reference for monitoring system performance and resource usage on a Linux system.

---

#### Basic System Monitoring

1. **System Uptime**:
    ```sh
    uptime
    ```
    - Displays system uptime, number of users, and load averages.

2. **System Load and CPU Usage**:
    - Use `top` to monitor real-time system load and CPU usage:
      ```sh
      top
      ```
    - Enhanced version of `top`:
      ```sh
      htop
      ```
    - Display CPU information:
      ```sh
      lscpu
      ```

3. **Memory Usage**:
    - Display memory usage:
      ```sh
      free -h
      ```
    - Display memory information:
      ```sh
      vmstat
      ```

4. **Disk Usage**:
    - Display disk usage:
      ```sh
      df -h
      ```
    - Display disk space usage by directory:
      ```sh
      du -h --max-depth=1 /path/to/directory
      ```

#### Advanced System Monitoring

1. **Detailed CPU and Memory Usage**:
    - Use `pidstat` for per-process CPU and memory usage:
      ```sh
      sudo apt install sysstat  # Debian/Ubuntu
      sudo yum install sysstat  # Red Hat/CentOS
      pidstat
      ```
    - Example for monitoring a specific process:
      ```sh
      pidstat -p <PID>
      ```

2. **I/O Statistics**:
    - Use `iostat` to monitor I/O device load:
      ```sh
      iostat
      ```
    - Example for monitoring every 5 seconds:
      ```sh
      iostat -x 5
      ```

3. **Network Statistics**:
    - Use `netstat` to display network connections and statistics:
      ```sh
      netstat -tuln
      ```
    - Use `ss` as an alternative to `netstat`:
      ```sh
      ss -tuln
      ```
    - Display network interface statistics:
      ```sh
      ifconfig
      ```
    - Use `ip` as an alternative to `ifconfig`:
      ```sh
      ip a
      ```

4. **Disk I/O Monitoring**:
    - Use `iotop` to monitor disk I/O:
      ```sh
      sudo apt install iotop  # Debian/Ubuntu
      sudo yum install iotop  # Red Hat/CentOS
      sudo iotop
      ```

5. **System Logs**:
    - View system logs:
      ```sh
      sudo journalctl -xe
      ```
    - View kernel ring buffer:
      ```sh
      dmesg
      ```

#### Monitoring Tools

1. **sar**: System activity report.
    - Install `sysstat` package:
      ```sh
      sudo apt install sysstat  # Debian/Ubuntu
      sudo yum install sysstat  # Red Hat/CentOS
      ```
    - Enable data collection:
      ```sh
      sudo systemctl enable sysstat
      sudo systemctl start sysstat
      ```
    - Display CPU usage:
      ```sh
      sar -u 1 3
      ```
    - Display memory usage:
      ```sh
      sar -r 1 3
      ```

2. **nmon**: Interactive system performance monitoring tool.
    - Install `nmon`:
      ```sh
      sudo apt install nmon  # Debian/Ubuntu
      sudo yum install nmon  # Red Hat/CentOS
      ```
    - Start `nmon`:
      ```sh
      nmon
      ```

3. **glances**: Cross-platform monitoring tool.
    - Install `glances`:
      ```sh
      sudo apt install glances  # Debian/Ubuntu
      sudo yum install glances  # Red Hat/CentOS
      ```
    - Start `glances`:
      ```sh
      glances
      ```

4. **Collectd**: System statistics collection daemon.
    - Install `collectd`:
      ```sh
      sudo apt install collectd  # Debian/Ubuntu
      sudo yum install collectd  # Red Hat/CentOS
      ```
    - Start `collectd`:
      ```sh
      sudo systemctl start collectd
      sudo systemctl enable collectd
      ```

5. **Prometheus and Grafana**: Advanced monitoring and alerting toolkit.
    - **Prometheus**:
        - Install and configure Prometheus.
    - **Grafana**:
        - Install and configure Grafana for data visualization.

By using this study sheet, new starters can efficiently monitor system performance and resource usage on a Linux system, ensuring optimal operation and quick troubleshooting.
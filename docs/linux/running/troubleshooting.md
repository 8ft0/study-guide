### Debugging/Troubleshooting Skills Study Sheet

**Purpose**: To provide a quick reference for debugging and troubleshooting at the application, infrastructure/system, and Linux levels.

---

#### Application Level Debugging

1. **Identify Symptoms**:
    - Check logs: 
      ```sh
      tail -f /var/log/app.log
      ```
    - Look for error messages or stack traces.

2. **Check Application Status**:
    - Verify if the application is running:
      ```sh
      ps aux | grep <application-name>
      ```

3. **Restart the Application**:
    - Use system service manager (e.g., `systemctl`):
      ```sh
      sudo systemctl restart <application-name>
      ```
    - Check status:
      ```sh
      sudo systemctl status <application-name>
      ```

4. **Inspect Logs**:
    - Application logs:
      ```sh
      tail -n 100 /var/log/<application>.log
      ```
    - System logs:
      ```sh
      journalctl -u <application-name>
      ```

5. **Trace Issues**:
    - Use `strace` to trace system calls:
      ```sh
      strace -p <pid>
      ```

6. **Check Dependencies**:
    - Verify all dependencies are installed and properly configured.

7. **Network Issues**:
    - Check network connectivity if the application relies on network services.
      ```sh
      ping <service-host>
      telnet <service-host> <port>
      ```

8. **Resource Usage**:
    - Check resource usage (CPU, memory):
      ```sh
      top
      htop
      ```

#### Infrastructure/System Level Troubleshooting

1. **IO Issues**:
    - Check disk usage:
      ```sh
      df -h
      ```
    - Monitor disk IO:
      ```sh
      iostat -x 1
      ```

2. **Network/Connectivity Issues**:
    - Check network interfaces:
      ```sh
      ip a
      ```
    - Test connectivity:
      ```sh
      ping <hostname>
      traceroute <hostname>
      ```
    - Inspect network traffic:
      ```sh
      tcpdump -i eth0
      ```

3. **Resource Exhaustion**:
    - Check file descriptors usage:
      ```sh
      lsof | wc -l
      ```
    - Increase file descriptor limits if necessary:
      ```sh
      ulimit -n 4096
      ```

4. **CPU and Memory Usage**:
    - Monitor CPU usage:
      ```sh
      top
      ```
    - Check memory usage:
      ```sh
      free -m
      vmstat 1
      ```

5. **Check System Logs**:
    - System logs:
      ```sh
      dmesg
      tail -f /var/log/syslog
      ```
    - Check for hardware errors, kernel messages, etc.

#### Linux Level Troubleshooting

1. **Processes and Threads**:
    - List all processes:
      ```sh
      ps aux
      ```
    - Check specific process details:
      ```sh
      ps -ef | grep <process-name>
      ```
    - Monitor threads:
      ```sh
      top -H -p <pid>
      ```

2. **Memory Usage/Allocation**:
    - Check memory usage:
      ```sh
      free -m
      ```
    - Detailed memory info:
      ```sh
      cat /proc/meminfo
      ```
    - Check memory usage by process:
      ```sh
      pmap -x <pid>
      ```

3. **Disk Usage**:
    - Check disk usage:
      ```sh
      df -h
      ```
    - Check inode usage:
      ```sh
      df -i
      ```
    - Find large files:
      ```sh
      find / -type f -size +100M
      ```

4. **Performance Monitoring**:
    - Real-time performance monitoring:
      ```sh
      top
      htop
      ```
    - System performance statistics:
      ```sh
      sar -u 1 10
      ```

5. **Kernel Logs**:
    - Check kernel ring buffer:
      ```sh
      dmesg
      ```
    - Monitor kernel logs:
      ```sh
      tail -f /var/log/kern.log
      ```

6. **System Resource Limits**:
    - Check resource limits:
      ```sh
      ulimit -a
      ```
    - Increase limits if necessary:
      ```sh
      ulimit -n 4096
      ```

#### General Troubleshooting Tips

1. **Document Everything**:
    - Keep detailed notes on what was checked and any changes made.
   
2. **Use a Systematic Approach**:
    - Follow a logical and structured troubleshooting process to avoid missing steps.

3. **Leverage Tools and Utilities**:
    - Use appropriate tools for each layer of troubleshooting (e.g., `top`, `htop`, `strace`, `tcpdump`).

4. **Consult Documentation**:
    - Refer to application and system documentation for specific error codes and troubleshooting steps.

By using this study sheet, new starters can effectively diagnose and resolve issues at the application, infrastructure/system, and Linux levels, ensuring smooth operation and minimal downtime.
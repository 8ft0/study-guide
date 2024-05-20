### Linux Process Management Cheat Sheet

**Purpose**: To provide a quick reference for managing processes on a Linux system.

---

#### Viewing Processes

1. **List Running Processes**:
    ```sh
    ps aux
    ```
    - Common columns:
      - `USER`: User who owns the process.
      - `PID`: Process ID.
      - `%CPU`: CPU usage.
      - `%MEM`: Memory usage.
      - `COMMAND`: Command that started the process.

2. **Interactive Process Viewer**:
    ```sh
    top
    ```
    - Press `q` to quit.
    - `htop` (an enhanced version of `top`):
      ```sh
      sudo apt install htop  # Debian/Ubuntu
      sudo yum install htop  # Red Hat/CentOS
      htop
      ```
    - Use arrow keys to navigate, `F10` to quit.

3. **Tree View of Processes**:
    ```sh
    pstree
    ```
    - Include PIDs:
      ```sh
      pstree -p
      ```

#### Managing Processes

1. **Start a Process**:
    ```sh
    <command>
    ```
    - Start in the background:
      ```sh
      <command> &
      ```

2. **Foreground and Background Processes**:
    - Send a running process to the background:
      ```sh
      <Ctrl+Z>
      bg %<job-number>
      ```
    - Bring a background process to the foreground:
      ```sh
      fg %<job-number>
      ```
    - List jobs:
      ```sh
      jobs
      ```

3. **Kill a Process**:
    - Gracefully terminate (SIGTERM):
      ```sh
      kill <PID>
      ```
    - Forcefully terminate (SIGKILL):
      ```sh
      kill -9 <PID>
      ```
    - Kill by process name:
      ```sh
      pkill <process-name>
      ```
    - Kill all processes owned by a user:
      ```sh
      pkill -u <username>
      ```

4. **Sending Signals to Processes**:
    - List all signals:
      ```sh
      kill -l
      ```
    - Send a specific signal (e.g., SIGHUP):
      ```sh
      kill -HUP <PID>
      ```

#### Monitoring and Controlling Resource Usage

1. **Limit CPU Usage**:
    - Use `cpulimit` to restrict CPU usage:
      ```sh
      sudo apt install cpulimit  # Debian/Ubuntu
      sudo yum install epel-release && sudo yum install cpulimit  # Red Hat/CentOS
      sudo cpulimit -p <PID> -l <percentage>
      ```

2. **Limit Memory Usage**:
    - Use `cgroups` to restrict memory usage:
      ```sh
      sudo cgcreate -g memory:/mygroup
      sudo cgset -r memory.limit_in_bytes=100M mygroup
      sudo cgexec -g memory:/mygroup <command>
      ```

3. **Monitor Process Resource Usage**:
    - Check CPU and memory usage of a process:
      ```sh
      top -p <PID>
      ```
    - Use `pidstat` for detailed statistics:
      ```sh
      sudo apt install sysstat  # Debian/Ubuntu
      sudo yum install sysstat  # Red Hat/CentOS
      pidstat -p <PID>
      ```

#### Process Scheduling

1. **Change Process Priority**:
    - View current priority (nice value):
      ```sh
      ps -l -p <PID>
      ```
    - Start a process with a specific nice value:
      ```sh
      nice -n <nice-value> <command>
      ```
    - Change the priority of an existing process:
      ```sh
      renice <nice-value> -p <PID>
      ```

2. **Real-time Process Monitoring**:
    - Use `watch` to execute a command periodically:
      ```sh
      watch -n <interval> <command>
      ```

#### Process Management Tools

1. **strace**: Trace system calls and signals.
   ```sh
   strace -p <PID>
   ```

2. **lsof**: List open files associated with processes.
   ```sh
   lsof -p <PID>
   ```

3. **pgrep**: Find processes by name.
   ```sh
   pgrep <process-name>
   ```

4. **pkill**: Send signals to processes by name.
   ```sh
   pkill <process-name>
   ```

By using this cheat sheet, new starters can efficiently manage processes on a Linux system, ensuring proper control over system resources and processes.
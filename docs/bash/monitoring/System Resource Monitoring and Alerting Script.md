# System Resource Monitoring and Alerting Script

### Description:
You are required to write a shell script that monitors CPU and memory usage on a system, and sends alerts when usage exceeds specified thresholds. The script should run continuously and log its activities.

### Requirements:
1. **Monitor CPU and Memory Usage**:
   - The script should check the CPU and memory usage at regular intervals (e.g., every 5 seconds).
   - If the CPU or memory usage exceeds specified thresholds, the script should log a warning message.

2. **Logging**:
   - The script should log its activities to a file named `system_usage.log` in the following format:
     ```yaml
     YYYY-MM-DD HH:MM:SS - [LEVEL] Message
     ```
     - `YYYY-MM-DD` is the date.
     - `HH:MM:SS` is the time.
     - `[LEVEL]` is the log level (`INFO`, `WARNING`).
     - `Message` is the log message.

3. **Command-line Arguments**:
   - The script should accept command-line arguments to specify the CPU and memory usage thresholds (in percentage).
   - If the thresholds are not provided, they should default to 75% for CPU and 80% for memory.

4. **Continuous Monitoring**:
   - The script should run continuously, checking the CPU and memory usage at regular intervals.

### Input:
- Command-line arguments specifying the CPU and memory usage thresholds (in percentage).

### Output:
- A log file named `system_usage.log` containing information and warning messages about CPU and memory usage.

### Example:
If the specified thresholds are 75% for CPU and 80% for memory, and the system usage is as follows:

```yaml
CPU usage: 65%
Memory usage: 85%
```

The log file should contain entries similar to:
```yaml
2024-05-18 14:00:00 - [INFO] Checked CPU usage: 65%
2024-05-18 14:00:00 - [WARNING] Memory usage is 85%, which exceeds the threshold of 80%
```

### Constraints:
- Your script should be written in bash.
- The script should handle cases where the thresholds are not provided and default to 75% for CPU and 80% for memory.
- Ensure the script runs efficiently to be suitable for continuous monitoring.

### Submission:
Submit your bash script file with the name `resource_monitor.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Default thresholds
DEFAULT_CPU_THRESHOLD=75
DEFAULT_MEM_THRESHOLD=80

# Get the thresholds from command-line arguments or use the defaults
CPU_THRESHOLD=${1:-$DEFAULT_CPU_THRESHOLD}
MEM_THRESHOLD=${2:-$DEFAULT_MEM_THRESHOLD}

# Log file
LOG_FILE="system_usage.log"

# Function to log messages
log_message() {
  local level=$1
  local message=$2
  echo "$(date '+%Y-%m-%d %H:%M:%S') - [$level] $message" >> $LOG_FILE
}

# Function to check CPU and memory usage
check_usage() {
  cpu_usage=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
  mem_usage=$(free | grep Mem | awk '{print $3/$2 * 100.0}')
  
  log_message "INFO" "Checked CPU usage: ${cpu_usage}%"
  log_message "INFO" "Checked memory usage: ${mem_usage}%"
  
  if (( $(echo "$cpu_usage > $CPU_THRESHOLD" |bc -l) )); then
    log_message "WARNING" "CPU usage is ${cpu_usage}%, which exceeds the threshold of ${CPU_THRESHOLD}%"
  fi
  
  if (( $(echo "$mem_usage > $MEM_THRESHOLD" |bc -l) )); then
    log_message "WARNING" "Memory usage is ${mem_usage}%, which exceeds the threshold of ${MEM_THRESHOLD}%"
  fi
}

# Run the check_usage function continuously at regular intervals
while true; do
  check_usage
  sleep 5
done
```

### Explanation:

1. **Set default thresholds**: The script sets default threshold values for CPU (75%) and memory (80%) usage.

2. **Get thresholds from command-line arguments**: It checks if thresholds for CPU and memory are provided as command-line arguments. If not, it uses the default values.

3. **Log file setup**: The script defines a log file `system_usage.log` and a function `log_message` to handle logging.

4. **Check CPU and memory usage**: The script uses `top` and `free` commands to get the CPU and memory usage, respectively, and logs the current usage as `INFO` messages.

5. **Check against thresholds**: If the CPU or memory usage exceeds the specified thresholds, it logs a `WARNING` message.

6. **Continuous monitoring**: The script runs the `check_usage` function in a continuous loop, checking the usage every 5 seconds.

This solution is designed to run continuously and efficiently, making it suitable for real-time monitoring of system resources.
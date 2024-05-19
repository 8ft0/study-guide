## Challenge Name: Disk Space Monitoring Script

### Description:
You are tasked with creating a shell script that monitors disk space usage on a system and sends alerts when the usage exceeds a specified threshold. The script should be designed to run periodically and log its activities.

### Requirements:
1. **Monitor Disk Space Usage**:
   - The script should check the disk space usage of all mounted filesystems.
   - If any filesystem's usage exceeds a specified threshold (e.g., 80%), the script should log a warning message.

2. **Logging**:
   - The script should log its activities to a file named `disk_usage.log` in the following format:
     ```yaml
     YYYY-MM-DD HH:MM:SS - [LEVEL] Message
     ```
     - `YYYY-MM-DD` is the date.
     - `HH:MM:SS` is the time.
     - `[LEVEL]` is the log level (`INFO`, `WARNING`).
     - `Message` is the log message.

3. **Command-line Arguments**:
   - The script should accept a command-line argument to specify the usage threshold (in percentage).
   - If the threshold is not provided, it should default to 80%.

4. **Periodic Execution**:
   - The script should be designed to be run periodically (e.g., via `cron`).

### Input:
- A command-line argument specifying the usage threshold (in percentage).

### Output:
- A log file named `disk_usage.log` containing information and warning messages about disk space usage.

### Example:
If the specified threshold is 80%, and the disk usage is as follows:

```yaml
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   35G   15G  70% /
/dev/sda2        20G   18G    2G  90% /home
```

The log file should contain entries similar to:
```yaml
2024-05-18 14:00:00 - [INFO] Checked disk usage for /dev/sda1: 70%
2024-05-18 14:00:00 - [WARNING] Disk usage for /dev/sda2 is 90%, which exceeds the threshold of 80%
```

### Constraints:
- Your script should be written in bash.
- The script should handle cases where the threshold is not provided and default to 80%.
- Ensure the script runs efficiently to be suitable for periodic execution.

### Submission:
Submit your bash script file with the name `disk_space_monitor.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Default threshold
DEFAULT_THRESHOLD=80

# Get the threshold from the command-line argument or use the default
THRESHOLD=${1:-$DEFAULT_THRESHOLD}

# Log file
LOG_FILE="disk_usage.log"

# Function to log messages
log_message() {
  local level=$1
  local message=$2
  echo "$(date '+%Y-%m-%d %H:%M:%S') - [$level] $message" >> $LOG_FILE
}

# Check disk usage for each mounted filesystem
df -H | awk 'NR>1' | while read -r line; do
  usage=$(echo $line | awk '{print $5}' | tr -d '%')
  filesystem=$(echo $line | awk '{print $1}')
  mount_point=$(echo $line | awk '{print $6}')
  
  log_message "INFO" "Checked disk usage for $filesystem ($mount_point): $usage%"
  
  if [ $usage -ge $THRESHOLD ]; then
    log_message "WARNING" "Disk usage for $filesystem ($mount_point) is ${usage}%, which exceeds the threshold of ${THRESHOLD}%"
  fi
done

```

### Explanation:

1. **Set default threshold**: The script sets a default threshold value of 80%.

2. **Get threshold from command-line argument**: It checks if a threshold is provided as a command-line argument. If not, it uses the default value.

3. **Log file setup**: The script defines a log file `disk_usage.log` and a function `log_message` to handle logging.

4. **Check disk usage**: The script uses the `df -H` command to get the disk usage of all mounted filesystems, skipping the header line.

5. **Log disk usage**: For each filesystem, it logs the current usage as an `INFO` message.

6. **Check against threshold**: If the usage exceeds the specified threshold, it logs a `WARNING` message.

This solution is designed to be efficient and suitable for periodic execution via `cron`. It ensures that disk usage is monitored and alerts are logged when usage exceeds the specified threshold.
## Challenge Name: System Resource Monitoring and Alerting

### Description:
You are required to write a shell script that monitors the system's CPU and memory usage. If the usage exceeds specified thresholds, the script should log an alert message to a file and send an email notification.

### Requirements:
1. **Monitor system resources**:
   - Monitor CPU and memory usage at regular intervals (e.g., every 10 seconds).
   - If CPU usage exceeds 80% or memory usage exceeds 70%, log an alert and send an email.

2. **Log alerts**:
   - Log alert messages to a file named `system_alerts.log` in the following format:
     ```
     YYYY-MM-DD HH:MM:SS - ALERT: <resource> usage is <usage>%
     ```

3. **Send email notifications**:
   - Send an email with the alert message to a specified email address.

### Input:
- Thresholds for CPU (80%) and memory (70%) usage.
- Email address to send notifications to.

### Output:
- A log file named `system_alerts.log` containing alert messages.
- Email notifications sent to the specified email address when thresholds are exceeded.

### Example:
If CPU usage exceeds 80%, an alert message should be logged and an email should be sent:
```
2024-05-16 12:00:00 - ALERT: CPU usage is 85%
```

### Constraints:
- Your script should be written in bash.
- Assume the system has the `mail` utility installed for sending emails.
- The script should run continuously, monitoring resources at specified intervals.

### Submission:
Submit your bash script file with the name `monitor_system.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Email address to send alerts to
EMAIL="your_email@example.com"

# Thresholds
CPU_THRESHOLD=80
MEM_THRESHOLD=70

# Log file
LOG_FILE="system_alerts.log"

# Function to log alerts
log_alert() {
  local message=$1
  echo "$(date '+%Y-%m-%d %H:%M:%S') - ALERT: $message" >> $LOG_FILE
}

# Function to send email alerts
send_email() {
  local subject=$1
  local body=$2
  echo "$body" | mail -s "$subject" $EMAIL
}

# Monitor system resources
while true; do
  # Get CPU and memory usage
  CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
  MEM_USAGE=$(free | grep Mem | awk '{print $3/$2 * 100.0}')
  
  # Check CPU usage
  if (( $(echo "$CPU_USAGE > $CPU_THRESHOLD" | bc -l) )); then
    message="CPU usage is ${CPU_USAGE}%"
    log_alert "$message"
    send_email "CPU Usage Alert" "$message"
  fi
  
  # Check memory usage
  if (( $(echo "$MEM_USAGE > $MEM_THRESHOLD" | bc -l) )); then
    message="Memory usage is ${MEM_USAGE}%"
    log_alert "$message"
    send_email "Memory Usage Alert" "$message"
  fi
  
  # Wait for the next check
  sleep 10
done
```

### Explanation:

1. **Initialise variables**: Set the email address, CPU and memory usage thresholds, and the log file name.

2. **Log alerts**: Define a function `log_alert` that writes alert messages to the log file with a timestamp.

3. **Send email alerts**: Define a function `send_email` that sends an email with the alert message.

4. **Monitor system resources**: Use a `while true` loop to continuously monitor CPU and memory usage at 10-second intervals.
   - **CPU usage**: Calculate CPU usage using `top` and check if it exceeds the threshold. If so, log the alert and send an email.
   - **Memory usage**: Calculate memory usage using `free` and check if it exceeds the threshold. If so, log the alert and send an email.

5. **Wait for the next check**: Use `sleep 10` to wait 10 seconds before the next check.

This solution assumes the `mail` utility is installed and configured on the system. Adjustments may be needed based on specific requirements or system configurations.

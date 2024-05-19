## Challenge Name: Acme Service Health Check and Alert

### Description:
You are an SRE (Site Reliability Engineer) at Acme, responsible for maintaining the health of various services. Your task is to write a bash script that checks the health of a specified service by making HTTP requests to its health endpoint, logs the response times, and sends an alert email if the response time exceeds a certain threshold.

### Requirements:
1. **Health check**: Make HTTP GET requests to the service's health endpoint at regular intervals.
2. **Log response times**: Record the response times and status codes in a log file.
3. **Threshold alert**: If the response time exceeds a specified threshold, send an alert email.
4. **Configuration**: Use a configuration file to specify the service URL, interval, threshold, and email address.

### Input:
- A configuration file `health_check.conf` with the following content:
  ```
  SERVICE_URL="http://example.com/health"
  CHECK_INTERVAL=60  # seconds
  RESPONSE_THRESHOLD=2000  # milliseconds
  ALERT_EMAIL="alert@example.com"
  ```

### Output:
- A log file named `health_check.log` containing the timestamp, response time, and status code of each health check.
- An email alert sent to the specified email address if the response time exceeds the threshold.

### Example:
Suppose the configuration file contains:
```
SERVICE_URL="http://example.com/health"
CHECK_INTERVAL=60
RESPONSE_THRESHOLD=2000
ALERT_EMAIL="alert@example.com"
```

The log file `health_check.log` might look like:
```
2024-05-18 12:00:00 1800 200
2024-05-18 12:01:00 2100 200
```

An email alert would be sent if the response time exceeds 2000 milliseconds.

### Constraints:
- Your script should be written in bash.
- Assume the service health endpoint returns a standard HTTP response.
- Use standard Unix tools like `curl`, `awk`, `date`, and `mail`.

### Submission:
Submit your bash script file with the name `service_health_check.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Source the configuration file
source health_check.conf

# Initialize the log file
log_file="health_check.log"

# Function to send alert email
send_alert() {
  local response_time=$1
  echo "Service response time exceeded threshold: ${response_time}ms" | mail -s "Service Health Alert" $ALERT_EMAIL
}

# Function to perform health check
perform_health_check() {
  while true; do
    # Record the start time
    start_time=$(date +%s%3N)
    
    # Make the HTTP request and capture the response time and status code
    response=$(curl -o /dev/null -s -w "%{http_code}" $SERVICE_URL)
    status_code=$?
    end_time=$(date +%s%3N)
    response_time=$((end_time - start_time))
    
    # Log the result
    echo "$(date '+%Y-%m-%d %H:%M:%S') ${response_time} ${response}" >> $log_file
    
    # Check if the response time exceeds the threshold
    if [ $response_time -gt $RESPONSE_THRESHOLD ]; then
      send_alert $response_time
    fi
    
    # Wait for the next interval
    sleep $CHECK_INTERVAL
  done
}

# Start the health check
perform_health_check
```

### Explanation:

1. **Source the configuration file**: The script sources `health_check.conf` to load the service URL, check interval, response threshold, and alert email address.

2. **Initialise the log file**: The script sets up a log file `health_check.log` to record health check results.

3. **Function to send alert email**: The `send_alert` function sends an email if the response time exceeds the threshold.

4. **Function to perform health check**: The `perform_health_check` function makes HTTP GET requests to the service's health endpoint, records the response time and status code, logs the result, checks if the response time exceeds the threshold, and sends an alert if necessary.

5. **Start the health check**: The script calls `perform_health_check` to start the health check process, which runs indefinitely at the specified intervals.

This solution assumes the health check configuration file is correctly formatted and the service health endpoint returns standard HTTP responses. Adjustments may be needed based on specific requirements or variations in input.
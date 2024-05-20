## Log File and Tarball Manipulation

### Description:
You are provided with a tarball (`logs.tar.gz`) containing multiple log files. Your task is to write a shell script that extracts the tarball, processes the log files, and generates a summary report.

### Requirements:
1. **Extract the tarball**: Extract `logs.tar.gz` to a directory named `logs`.
2. **Process log files**: Each log file contains multiple lines with entries in the following format:
   ```
   YYYY-MM-DD HH:MM:SS [LEVEL] Message
   ```
   - `YYYY-MM-DD` is the date.
   - `HH:MM:SS` is the time.
   - `[LEVEL]` is the log level (`INFO`, `WARNING`, `ERROR`).
   - `Message` is the log message.

3. **Generate summary report**:
   - Count the number of log entries for each log level (INFO, WARNING, ERROR) across all log files.
   - Identify the most recent log entry (based on date and time) for each log level.

### Input:
- A tarball file named `logs.tar.gz` containing multiple log files.

### Output:
- A summary report printed to the console with the following format:
  ```
  Log Summary Report
  ==================
  Total INFO entries: <number>
  Total WARNING entries: <number>
  Total ERROR entries: <number>

  Most recent INFO entry: <YYYY-MM-DD HH:MM:SS [LEVEL] Message>
  Most recent WARNING entry: <YYYY-MM-DD HH:MM:SS [LEVEL] Message>
  Most recent ERROR entry: <YYYY-MM-DD HH:MM:SS [LEVEL] Message>
  ```

### Example:
Suppose `logs.tar.gz` contains two log files `log1.txt` and `log2.txt` with the following content:

**log1.txt**:
```
2024-05-16 12:00:00 [INFO] System started
2024-05-16 12:01:00 [ERROR] Failed to connect to database
2024-05-16 12:02:00 [WARNING] Low disk space
```

**log2.txt**:
```
2024-05-16 12:03:00 [INFO] User login
2024-05-16 12:04:00 [WARNING] High memory usage
2024-05-16 12:05:00 [ERROR] Service crashed
```

The summary report should be:
```
Log Summary Report
==================
Total INFO entries: 2
Total WARNING entries: 2
Total ERROR entries: 2

Most recent INFO entry: 2024-05-16 12:03:00 [INFO] User login
Most recent WARNING entry: 2024-05-16 12:04:00 [WARNING] High memory usage
Most recent ERROR entry: 2024-05-16 12:05:00 [ERROR] Service crashed
```

### Constraints:
- Your script should be written in bash.
- Assume the tarball always contains valid log files in the specified format.
- Your script should handle an arbitrary number of log files within the tarball.

### Submission:
Submit your bash script file with the name `process_logs.sh`.

---


Here's a bash script solution for the described challenge:

```bash
#!/bin/bash

# Extract the tarball
mkdir -p logs
tar -xzvf logs.tar.gz -C logs

# Initialize counters
total_info=0
total_warning=0
total_error=0

# Initialize most recent log entries
recent_info=""
recent_warning=""
recent_error=""

# Function to compare and update the most recent log entry
update_recent() {
  local level=$1
  local entry=$2
  local datetime=$(echo "$entry" | awk '{print $1 " " $2}')
  case $level in
    INFO)
      if [[ -z $recent_info || $datetime > $(echo "$recent_info" | awk '{print $1 " " $2}') ]]; then
        recent_info=$entry
      fi
      ;;
    WARNING)
      if [[ -z $recent_warning || $datetime > $(echo "$recent_warning" | awk '{print $1 " " $2}') ]]; then
        recent_warning=$entry
      fi
      ;;
    ERROR)
      if [[ -z $recent_error || $datetime > $(echo "$recent_error" | awk '{print $1 " " $2}') ]]; then
        recent_error=$entry
      fi
      ;;
  esac
}

# Process each log file
for log_file in logs/*; do
  while IFS= read -r line; do
    level=$(echo "$line" | awk '{print $3}' | tr -d '[]')
    case $level in
      INFO)
        ((total_info++))
        update_recent INFO "$line"
        ;;
      WARNING)
        ((total_warning++))
        update_recent WARNING "$line"
        ;;
      ERROR)
        ((total_error++))
        update_recent ERROR "$line"
        ;;
    esac
  done < "$log_file"
done

# Generate summary report
echo "Log Summary Report"
echo "=================="
echo "Total INFO entries: $total_info"
echo "Total WARNING entries: $total_warning"
echo "Total ERROR entries: $total_error"
echo
echo "Most recent INFO entry: $recent_info"
echo "Most recent WARNING entry: $recent_warning"
echo "Most recent ERROR entry: $recent_error"
```

### Explanation:

1. **Extract the tarball**: The script creates a `logs` directory and extracts `logs.tar.gz` into it.

2. **Initialise counters and most recent log entries**: Variables are set up to count log levels and track the most recent entries.

3. **Update recent function**: A helper function `update_recent` compares timestamps and updates the most recent log entry for each level.

4. **Process each log file**: The script iterates through each log file in the `logs` directory, reads each line, and updates counters and recent entries based on log levels.

5. **Generate summary report**: The script prints the total counts and most recent log entries for each log level.

This script assumes the log files are correctly formatted and the tarball is always named `logs.tar.gz`. Adjustments may be needed based on specific requirements or variations in input.

---

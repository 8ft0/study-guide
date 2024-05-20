# Log File Analysis and Archive

### Description:
You are given a directory containing multiple log files. Your task is to write a shell script that processes these log files to extract specific information, generates a summary report, and then archives the log files into a tarball.

### Requirements:
1. **Process log files**: Each log file contains multiple lines with entries in the following format:
    ```
    YYYY-MM-DD HH:MM:SS [LEVEL] Message
    ```
    - `YYYY-MM-DD` is the date.
    - `HH:MM:SS` is the time.
    - `[LEVEL]` is the log level (`INFO`, `WARNING`, `ERROR`).
    - `Message` is the log message.

2. **Generate summary report**:
    - Count the number of log entries for each log level (INFO, WARNING, ERROR) across all log files.
    - Identify the date with the highest number of log entries.

3. **Archive log files**: After processing, archive all log files into a tarball named `processed_logs.tar.gz`.

### Input:
- A directory named `log_files` containing multiple log files.

### Output:
- A summary report printed to the console with the following format:
  ```
  Log Summary Report
  ==================
  Total INFO entries: <number>
  Total WARNING entries: <number>
  Total ERROR entries: <number>

  Date with highest number of entries: <YYYY-MM-DD> with <number> entries
  ```
- A tarball named `processed_logs.tar.gz` containing all the log files from the `log_files` directory.

### Example:
Suppose the `log_files` directory contains two log files `log1.txt` and `log2.txt` with the following content:

**log1.txt**:
```
2024-05-16 12:00:00 [INFO] System started
2024-05-16 12:01:00 [ERROR] Failed to connect to database
2024-05-16 12:02:00 [WARNING] Low disk space
```

**log2.txt**:
```
2024-05-16 12:03:00 [INFO] User login
2024-05-17 12:04:00 [WARNING] High memory usage
2024-05-17 12:05:00 [ERROR] Service crashed
```

The summary report should be:
```
Log Summary Report
==================
Total INFO entries: 2
Total WARNING entries: 2
Total ERROR entries: 2

Date with highest number of entries: 2024-05-16 with 3 entries
```

### Constraints:
- Your script should be written in bash.
- Assume the log files always contain valid entries in the specified format.
- Your script should handle an arbitrary number of log files in the `log_files` directory.

### Submission:
Submit your bash script file with the name `analyze_and_archive_logs.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Initialize counters
total_info=0
total_warning=0
total_error=0

declare -A date_entries

# Process each log file
for log_file in log_files/*; do
  while IFS= read -r line; do
    level=$(echo "$line" | awk '{print $3}' | tr -d '[]')
    date=$(echo "$line" | awk '{print $1}')
    
    # Count log levels
    case $level in
      INFO)
        ((total_info++))
        ;;
      WARNING)
        ((total_warning++))
        ;;
      ERROR)
        ((total_error++))
        ;;
    esac

    # Count entries per date
    if [ -n "$date" ]; then
      ((date_entries["$date"]++))
    fi
  done < "$log_file"
done

# Identify the date with the highest number of log entries
max_entries=0
max_date=""
for date in "${!date_entries[@]}"; do
  if [ ${date_entries["$date"]} -gt $max_entries ]; then
    max_entries=${date_entries["$date"]}
    max_date=$date
  fi
done

# Generate summary report
echo "Log Summary Report"
echo "=================="
echo "Total INFO entries: $total_info"
echo "Total WARNING entries: $total_warning"
echo "Total ERROR entries: $total_error"
echo
echo "Date with highest number of entries: $max_date with $max_entries entries"

# Archive log files into a tarball
tar -czvf processed_logs.tar.gz -C log_files .

```

### Explanation:

1. **Initialise counters and date entries**: Variables and an associative array are set up to count log levels and track the number of entries per date.

2. **Process each log file**: The script iterates through each log file in the `log_files` directory, reads each line, updates counters, and counts entries per date.

3. **Identify date with the highest number of entries**: The script determines the date with the most log entries by iterating through the `date_entries` associative array.

4. **Generate summary report**: The script prints the total counts and the date with the highest number of log entries.

5. **Archive log files**: The script archives all log files from the `log_files` directory into a tarball named `processed_logs.tar.gz`.

This solution assumes the log files are correctly formatted and the directory is always named `log_files`. Adjustments may be needed based on specific requirements or variations in input.
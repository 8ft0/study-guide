# Log File Analysis with Error Distribution

### Description:
You are given a directory containing multiple log files. Your task is to write a shell script that analyses these log files to calculate the distribution of log entries per hour, specifically focusing on `ERROR` log entries. The script should generate a summary report showing the number of `ERROR` entries for each hour of the day.

### Requirements:
1. **Process log files**: Each log file contains multiple lines with entries in the following format:
    ```
    YYYY-MM-DD HH:MM:SS [LEVEL] Message
    ```
    - `YYYY-MM-DD` is the date.
    - `HH:MM:SS` is the time.
    - `[LEVEL]` is the log level (`INFO`, `WARNING`, `ERROR`).
    - `Message` is the log message.

2. **Generate error distribution report**:
    - Count the number of `ERROR` log entries for each hour of the day (00 to 23).
    - Output the distribution in a report format.

### Input:
- A directory named `log_files` containing multiple log files.

### Output:
- A summary report printed to the console with the following format:
  ```
  Error Distribution Report
  =========================
  Hour 00: <number of errors>
  Hour 01: <number of errors>
  ...
  Hour 23: <number of errors>
  ```

### Example:
Suppose the `log_files` directory contains two log files `log1.txt` and `log2.txt` with the following content:

**log1.txt**:
```
2024-05-16 12:00:00 [INFO] System started
2024-05-16 12:01:00 [ERROR] Failed to connect to database
2024-05-16 13:45:00 [WARNING] Low disk space
```

**log2.txt**:
```
2024-05-16 12:03:00 [INFO] User login
2024-05-16 12:04:00 [ERROR] Service crashed
2024-05-16 14:15:00 [ERROR] Disk full
```

The error distribution report should be:
```
Error Distribution Report
=========================
Hour 00: 0
Hour 01: 0
...
Hour 12: 2
Hour 13: 0
Hour 14: 1
...
Hour 23: 0
```

### Constraints:
- Your script should be written in bash.
- Assume the log files always contain valid entries in the specified format.
- Your script should handle an arbitrary number of log files in the `log_files` directory.

### Submission:
Submit your bash script file with the name `error_distribution_report.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Initialize an array to hold the count of errors for each hour
declare -a error_count
for i in {0..23}; do
  error_count[$i]=0
done

# Process each log file
for log_file in log_files/*; do
  while IFS= read -r line; do
    level=$(echo "$line" | awk '{print $3}' | tr -d '[]')
    if [ "$level" == "ERROR" ]; then
      hour=$(echo "$line" | awk '{print $2}' | cut -d':' -f1)
      ((error_count[hour]++))
    fi
  done < "$log_file"
done

# Generate error distribution report
echo "Error Distribution Report"
echo "========================="
for i in {0..23}; do
  printf "Hour %02d: %d\n" $i ${error_count[$i]}
done
```

### Explanation:

1. **Initialise an array to hold error counts**: The script sets up an array `error_count` with 24 elements (one for each hour) and initialises each element to 0.

2. **Process each log file**: The script iterates through each log file in the `log_files` directory, reads each line, checks if the log level is `ERROR`, extracts the hour from the timestamp, and increments the corresponding element in the `error_count` array.

3. **Generate error distribution report**: The script prints the error distribution report, showing the number of `ERROR` entries for each hour of the day.

This solution assumes the log files are correctly formatted and the directory is always named `log_files`. Adjustments may be needed based on specific requirements or variations in input.
## Log File Filtering and Compression

### Description:
You are given a directory containing multiple log files. Your task is to write a shell script that filters the log entries based on a specified log level, outputs these filtered entries to a new file, and then compresses this file into a zip archive.

### Requirements:
1. **Filter log entries**: Each log file contains multiple lines with entries in the following format:
   ```
   YYYY-MM-DD HH:MM:SS [LEVEL] Message
   ```
   - `YYYY-MM-DD` is the date.
   - `HH:MM:SS` is the time.
   - `[LEVEL]` is the log level (`INFO`, `WARNING`, `ERROR`).
   - `Message` is the log message.

2. **Generate filtered log file**:
   - Filter log entries based on a specified log level (e.g., `ERROR`).
   - Output these filtered entries to a new file named `filtered_logs.txt`.

3. **Compress filtered log file**:
   - Compress `filtered_logs.txt` into a zip archive named `filtered_logs.zip`.

### Input:
- A directory named `log_files` containing multiple log files.
- A specified log level to filter (e.g., `ERROR`).

### Output:
- A file named `filtered_logs.txt` containing the filtered log entries.
- A zip archive named `filtered_logs.zip` containing `filtered_logs.txt`.

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
2024-05-16 12:04:00 [WARNING] High memory usage
2024-05-16 12:05:00 [ERROR] Service crashed
```

If the specified log level is `ERROR`, the content of `filtered_logs.txt` should be:
```
2024-05-16 12:01:00 [ERROR] Failed to connect to database
2024-05-16 12:05:00 [ERROR] Service crashed
```

### Constraints:
- Your script should be written in bash.
- Assume the log files always contain valid entries in the specified format.
- Your script should handle an arbitrary number of log files in the `log_files` directory.

### Submission:
Submit your bash script file with the name `filter_and_compress_logs.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Check if the log level is specified
if [ -z "$1" ]; then
  echo "Usage: $0 <LOG_LEVEL>"
  exit 1
fi

LOG_LEVEL=$1

# Initialize the output file
output_file="filtered_logs.txt"
> $output_file

# Process each log file
for log_file in log_files/*; do
  while IFS= read -r line; do
    level=$(echo "$line" | awk '{print $3}' | tr -d '[]')
    if [ "$level" == "$LOG_LEVEL" ]; then
      echo "$line" >> $output_file
    fi
  done < "$log_file"
done

# Compress the filtered log file into a zip archive
zip filtered_logs.zip $output_file

echo "Filtered log entries have been saved to $output_file and compressed into filtered_logs.zip"
```

### Explanation:

1. **Check if the log level is specified**: The script requires a log level as an argument. If not provided, it displays usage information and exits.

2. **Initialise the output file**: The script creates or clears the `filtered_logs.txt` file to store filtered log entries.

3. **Process each log file**: The script iterates through each log file in the `log_files` directory, reads each line, and appends entries that match the specified log level to `filtered_logs.txt`.

4. **Compress the filtered log file**: The script compresses `filtered_logs.txt` into a zip archive named `filtered_logs.zip`.

5. **Completion message**: The script outputs a message indicating the filtered log entries have been saved and compressed.

This solution assumes the log files are correctly formatted and the directory is always named `log_files`. Adjustments may be needed based on specific requirements or variations in input.
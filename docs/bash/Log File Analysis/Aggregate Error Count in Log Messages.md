## Aggregate Error Count in Log Messages 

#### Problem Statement

You are given a log file where each line contains a timestamp, a severity level (INFO, WARNING, ERROR), and a message. Your task is to write a Bash script to parse the log file and count the number of `ERROR` messages, aggregating them based on the error message content.

#### Log File Format

Each log entry is in the format:
```
[timestamp] [severity] message
```
- `timestamp` is a string representing the time of the event.
- `severity` is one of `INFO`, `WARNING`, or `ERROR`.
- `message` is a string representing the event message.

#### Example Log File

```plaintext
[2023-05-20 12:00:00] INFO User logged in
[2023-05-20 12:01:00] WARNING Disk space low
[2023-05-20 12:02:00] ERROR Unable to connect to database
[2023-05-20 12:02:10] ERROR Unable to connect to database
[2023-05-20 12:03:00] INFO User logged out
[2023-05-20 12:04:00] ERROR Failed to load resource
[2023-05-20 12:04:05] ERROR Unable to connect to database
```

#### Output

The script should output the aggregated count of each unique error message:
```
Unable to connect to database: 3
Failed to load resource: 1
```

### Bash Script Solution

To solve this problem using a Bash script, you can use tools like `grep`, `awk`, and `sort` to filter, extract, and aggregate error counts based on the message content.

### Steps

1. Use `grep` to filter only `ERROR` level messages.
2. Use `awk` to extract the message content following the `ERROR` label.
3. Use `sort` and `uniq` to aggregate and count occurrences of each unique message.

### Bash Script Code

```bash
#!/bin/bash

# Define the log file
logfile="logfile.txt"

# Filter, extract, and count error messages
grep "ERROR" "$logfile" | cut -d ' ' -f 4- | sort | uniq -c | while read count message; do
    echo "$message: $count"
done
```

### Explanation

1. **Filtering Errors**: `grep "ERROR" "$logfile"` extracts only the lines that contain the word "ERROR".
2. **Extracting Messages**: `cut -d ' ' -f 4-` uses `cut` to split each line on spaces and extracts everything from the fourth field onward, which corresponds to the message after the severity level.
3. **Sorting and Counting**: `sort` sorts the error messages, and `uniq -c` counts each unique message.
4. **Output Formatting**: The `while read count message` loop reads the output from `uniq -c`, where `count` is the number of occurrences and `message` is the error message, and prints them in the desired format.

### Running the Script

1. Save the script to a file, for example, `count_errors.sh`.
2. Make it executable with `chmod +x count_errors.sh`.
3. Run the script with `./count_errors.sh`.

The script will then process the log file and output the count of each unique error message, providing a simple way to aggregate and summarize error occurrences in log files.
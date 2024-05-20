# Parse Logs and Count Events by Severity Level

#### Problem Statement

You are given a log file where each line contains a timestamp and a severity level (INFO, WARNING, ERROR). Your task is to write a Bash script to parse the log file and count the number of events for each severity level.

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
[2023-05-20 12:03:00] INFO User logged out
```

#### Output

The script should output the count of each severity level in the format:
```
INFO: 2
WARNING: 1
ERROR: 1
```

### Bash Script Solution

To solve this problem using a Bash script, we can use `grep` to filter lines by severity level and `wc -l` to count the number of lines for each severity.

### Steps

1. Use `grep` to find lines containing each severity level.
2. Count the number of lines found using `wc -l`.
3. Print the counts in the required format.

### Bash Script Code

```bash
#!/bin/bash

# Initialize counts
info_count=0
warning_count=0
error_count=0

# Read the log file
while IFS= read -r line; do
    # Extract the severity level
    severity=$(echo "$line" | awk '{print $2}')
    
    # Update the counts based on the severity level
    case $severity in
        INFO)
            info_count=$((info_count + 1))
            ;;
        WARNING)
            warning_count=$((warning_count + 1))
            ;;
        ERROR)
            error_count=$((error_count + 1))
            ;;
    esac
done < "logfile.txt"

# Print the counts
echo "INFO: $info_count"
echo "WARNING: $warning_count"
echo "ERROR: $error_count"
```

### Explanation

1. **Initialization**: We initialize variables to hold the counts for each severity level (`info_count`, `warning_count`, `error_count`).
2. **Reading the Log File**: We use a `while` loop to read the log file line by line. The `IFS= read -r line` command reads each line into the variable `line`.
3. **Extracting Severity Level**: We use `awk` to extract the second word of each line, which corresponds to the severity level.
4. **Updating Counts**: We use a `case` statement to increment the appropriate count variable based on the extracted severity level.
5. **Printing the Counts**: After processing all lines, we print the counts for each severity level.

### Example Usage

Save the script to a file, for example, `count_severity.sh`, and make it executable:

```bash
chmod +x count_severity.sh
```

Create a log file named `logfile.txt` with the example log entries:

```plaintext
[2023-05-20 12:00:00] INFO User logged in
[2023-05-20 12:01:00] WARNING Disk space low
[2023-05-20 12:02:00] ERROR Unable to connect to database
[2023-05-20 12:03:00] INFO User logged out
```

Run the script:

```bash
./count_severity.sh
```

The output should be:

```plaintext
INFO: 2
WARNING: 1
ERROR: 1
```

This script efficiently processes the log file and counts the number of events for each severity level using standard Bash tools and commands.
## Aggregate Error Count in Log Messages

#### Problem Statement

You are given a list of log entries where each log entry contains a timestamp, a severity level (INFO, WARNING, ERROR), and a message. Your task is to write a Python function to parse the logs and count the number of `ERROR` messages, aggregating them based on the error message content.

#### Function Signature

```python
def count_aggregated_errors(logs: List[str]) -> Dict[str, int]:
    pass
```

#### Input

- `logs`: A list of strings, each string representing a log entry in the format: `"[timestamp] [severity] message"`.

#### Output

- Return a dictionary with keys as unique error messages and values as the count of those messages.

#### Example

```python
logs = [
    "[2023-05-20 12:00:00] INFO User logged in",
    "[2023-05-20 12:01:00] WARNING Disk space low",
    "[2023-05-20 12:02:00] ERROR Unable to connect to database",
    "[2023-05-20 12:02:10] ERROR Unable to connect to database",
    "[2023-05-20 12:03:00] INFO User logged out",
    "[2023-05-20 12:04:00] ERROR Failed to load resource",
    "[2023-05-20 12:04:05] ERROR Unable to connect to database"
]

result = count_aggregated_errors(logs)
# result should be: {'Unable to connect to database': 3, 'Failed to load resource': 1}
```

#### Python Solution

To tackle this challenge, you can utilize Python's `collections.Counter` to efficiently count occurrences of each unique error message.

### Python Code

```python
from typing import List, Dict
from collections import Counter

def count_aggregated_errors(logs: List[str]) -> Dict[str, int]:
    error_messages = Counter()

    for log in logs:
        parts = log.split(' ', 3)  # Split into three parts to isolate the message
        if parts[1] == "ERROR":
            message = parts[3].strip()  # Get the actual message content
            error_messages[message] += 1

    return dict(error_messages)

# Example usage
logs = [
    "[2023-05-20 12:00:00] INFO User logged in",
    "[2023-05-20 12:01:00] WARNING Disk space low",
    "[2023-05-20 12:02:00] ERROR Unable to connect to database",
    "[2023-05-20 12:02:10] ERROR Unable to connect to database",
    "[2023-05-20 12:03:00] INFO User logged out",
    "[2023-05-20 12:04:00] ERROR Failed to load resource",
    "[2023-05-20 12:04:05] ERROR Unable to connect to database"
]

print(count_aggregated_errors(logs))
# Output: {'Unable to connect to database': 3, 'Failed to load resource': 1}
```

### Explanation

1. **Counter Initialization**: `error_messages` is initialized as a `Counter` object, which helps in automatically handling the counting of unique messages.
2. **Log Parsing**: Each log entry is split only three times (`log.split(' ', 3)`) to ensure that the full error message is captured without being split further. This captures the timestamp, severity, and the full message.
3. **Message Counting**: Only entries with a severity of "ERROR" are considered. The error message (`parts[3]`) is stripped of leading and trailing spaces and added to the `Counter`.
4. **Return Result**: The `Counter` object, which contains the counts of each unique error message, is converted to a dictionary and returned.

This approach efficiently processes the log entries and provides a detailed count of error messages, making it easy to identify common issues recorded in the logs.
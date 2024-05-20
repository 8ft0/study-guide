# Parse Logs and Count Events by Severity Level

#### Problem Statement

You are given a list of log entries, where each log entry contains a timestamp and a severity level (INFO, WARNING, ERROR). Your task is to parse the logs and count the number of events for each severity level.

#### Function Signature

```python
def count_events_by_severity(logs: List[str]) -> Dict[str, int]:
    pass
```

#### Input

- `logs`: A list of strings, where each string represents a log entry in the format: `"[timestamp] [severity] message"`.
  - `timestamp` is a string representing the time of the event.
  - `severity` is one of `INFO`, `WARNING`, or `ERROR`.
  - `message` is a string representing the event message.

#### Output

- Return a dictionary with keys as severity levels (`INFO`, `WARNING`, `ERROR`) and values as the count of events for each severity level.

#### Example

```python
logs = [
    "[2023-05-20 12:00:00] INFO User logged in",
    "[2023-05-20 12:01:00] WARNING Disk space low",
    "[2023-05-20 12:02:00] ERROR Unable to connect to database",
    "[2023-05-20 12:03:00] INFO User logged out"
]

result = count_events_by_severity(logs)
# result should be: {'INFO': 2, 'WARNING': 1, 'ERROR': 1}
```

#### Constraints

- The number of log entries will be between 1 and 10^5.
- Each log entry will follow the specified format.

### Reference Solution

To solve this problem, we can iterate through the list of log entries, parse each entry to extract the severity level, and maintain a count of each severity level using a dictionary.

### Steps

1. Initialize a dictionary to hold the counts for `INFO`, `WARNING`, and `ERROR`.
2. Iterate through each log entry in the input list.
3. For each log entry, split the string to extract the severity level.
4. Update the count for the extracted severity level in the dictionary.
5. Return the dictionary with the counts of each severity level.

### Reference Solution Code

```python
from typing import List, Dict

def count_events_by_severity(logs: List[str]) -> Dict[str, int]:
    severity_count = {
        'INFO': 0,
        'WARNING': 0,
        'ERROR': 0
    }
    
    for log in logs:
        # Assuming the log format is: "[timestamp] [severity] message"
        parts = log.split()
        severity = parts[1]  # severity is the second part of the split string
        
        if severity in severity_count:
            severity_count[severity] += 1
    
    return severity_count

# Example usage
logs = [
    "[2023-05-20 12:00:00] INFO User logged in",
    "[2023-05-20 12:01:00] WARNING Disk space low",
    "[2023-05-20 12:02:00] ERROR Unable to connect to database",
    "[2023-05-20 12:03:00] INFO User logged out"
]

print(count_events_by_severity(logs))  # Output: {'INFO': 2, 'WARNING': 1, 'ERROR': 1}
```

### Explanation

1. **Initialization**: We start by initializing a dictionary `severity_count` to keep track of the counts of `INFO`, `WARNING`, and `ERROR` events.
2. **Parsing Logs**: For each log entry in the list, we split the string to extract the severity level. The severity level is always the second part of the split string (`parts[1]`).
3. **Updating Counts**: We check if the extracted severity level is one of the keys in our dictionary. If it is, we increment the corresponding count.
4. **Return Result**: After processing all log entries, we return the `severity_count` dictionary, which contains the counts of each severity level.

This approach ensures that we efficiently count the severity levels with a time complexity of \(O(n)\), where \(n\) is the number of log entries.
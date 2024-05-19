## Challenge Name: SRE Challenge: Automated User Metrics Collection and Alerting

### Description:
As a Site Reliability Engineer (SRE) at Acme, you need to ensure the platform's stability and performance by monitoring user activity metrics and setting up automated alerts. Your task is to write a Python script that collects user metrics from a simulated API, processes the data to generate insights, and sets up an alerting mechanism for anomalous activity.

### Requirements:
1. **Collect user metrics**: Use a simulated API to collect user activity metrics. The API returns a JSON response with the following format:
   ```json
   {
     "timestamp": "YYYY-MM-DDTHH:MM:SSZ",
     "active_users": <number>,
     "new_videos": <number>,
     "likes": <number>,
     "comments": <number>,
     "shares": <number>
   }
   ```
   The script should collect data every minute for a specified duration (e.g., 10 minutes).

2. **Process data**:
   - Calculate the average number of active users per minute.
   - Identify the minute with the highest number of new videos uploaded.

3. **Set up alerting mechanism**:
   - Set a threshold for active users (e.g., 10000). If the number of active users exceeds this threshold at any minute, print an alert message.

### Input:
- Simulated API endpoint (e.g., `http://example.com/api/user_metrics`).
- Duration for data collection (e.g., 10 minutes).

### Output:
- Print a summary report with the average number of active users and the minute with the highest number of new videos.
- Print an alert message if the number of active users exceeds the threshold.

### Example:
Suppose the API returns the following data for three minutes:

**Minute 1**:
```json
{
  "timestamp": "2024-05-16T12:00:00Z",
  "active_users": 9500,
  "new_videos": 100,
  "likes": 1500,
  "comments": 200,
  "shares": 300
}
```

**Minute 2**:
```json
{
  "timestamp": "2024-05-16T12:01:00Z",
  "active_users": 10500,
  "new_videos": 120,
  "likes": 1600,
  "comments": 250,
  "shares": 350
}
```

**Minute 3**:
```json
{
  "timestamp": "2024-05-16T12:02:00Z",
  "active_users": 9800,
  "new_videos": 90,
  "likes": 1400,
  "comments": 180,
  "shares": 280
}
```

The summary report should be:
```
Summary Report
==============
Average active users per minute: 9933.33
Minute with highest number of new videos: 2024-05-16T12:01:00Z with 120 new videos
```

The alert message should be:
```
Alert: Active users exceeded threshold at 2024-05-16T12:01:00Z with 10500 active users
```

### Constraints:
- Your script should be written in Python.
- Assume the API always returns valid data in the specified format.

### Submission:
Submit your Python script file with the name `tiktok_sre_challenge.py`.

## Solution:

Here is a possible solution in the form of a Python script:

```python
import requests
import time
from datetime import datetime, timedelta

API_ENDPOINT = "http://example.com/api/user_metrics"
DURATION_MINUTES = 10
THRESHOLD_ACTIVE_USERS = 10000

def collect_metrics(api_endpoint, duration_minutes):
    end_time = datetime.utcnow() + timedelta(minutes=duration_minutes)
    metrics = []

    while datetime.utcnow() < end_time:
        response = requests.get(api_endpoint)
        data = response.json()
        metrics.append(data)
        time.sleep(60)

    return metrics

def process_metrics(metrics):
    total_active_users = 0
    highest_new_videos = 0
    highest_new_videos_time = ""

    for metric in metrics:
        total_active_users += metric["active_users"]
        if metric["new_videos"] > highest_new_videos:
            highest_new_videos = metric["new_videos"]
            highest_new_videos_time = metric["timestamp"]

    average_active_users = total_active_users / len(metrics)
    return average_active_users, highest_new_videos_time, highest_new_videos

def check_alerts(metrics, threshold):
    for metric in metrics:
        if metric["active_users"] > threshold:
            print(f"Alert: Active users exceeded threshold at {metric['timestamp']} with {metric['active_users']} active users")

def main():
    metrics = collect_metrics(API_ENDPOINT, DURATION_MINUTES)
    average_active_users, highest_new_videos_time, highest_new_videos = process_metrics(metrics)

    print("Summary Report")
    print("==============")
    print(f"Average active users per minute: {average_active_users:.2f}")
    print(f"Minute with highest number of new videos: {highest_new_videos_time} with {highest_new_videos} new videos")

    check_alerts(metrics, THRESHOLD_ACTIVE_USERS)

if __name__ == "__main__":
    main()
```

### Explanation:

1. **Collect metrics**: The `collect_metrics` function collects data from the API every minute for a specified duration and stores the metrics in a list.

2. **Process metrics**: The `process_metrics` function calculates the average number of active users per minute and identifies the minute with the highest number of new videos.

3. **Check alerts**: The `check_alerts` function checks if the number of active users exceeds the threshold and prints an alert message if it does.

4. **Main function**: The `main` function orchestrates the collection, processing, and alerting, and prints the summary report.

This solution assumes the API returns valid data and the endpoint is always accessible. Adjustments may be needed based on specific requirements or variations in input.


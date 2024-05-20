# Monitoring and Alerting for Acme Services

### Description:
As a Site Reliability Engineer (SRE) at Acme, your task is to ensure the smooth operation and performance of Acme's services. You need to create a monitoring and alerting system for a set of microservices to detect and respond to any performance issues or failures in real-time.

### Requirements:
1. **Service Metrics**: Collect and monitor key metrics for each microservice, such as:
   - CPU usage
   - Memory usage
   - Response time
   - Error rate

2. **Log Analysis**: Continuously analyze log files to detect patterns indicating potential issues, such as high error rates or slow response times.

3. **Alerts**: Set up alerts to notify the SRE team when certain thresholds are breached, for example:
   - CPU usage exceeds 80% for more than 5 minutes.
   - Memory usage exceeds 75% for more than 5 minutes.
   - Average response time exceeds 200ms for more than 3 minutes.
   - Error rate exceeds 1% for more than 2 minutes.

4. **Incident Response**: Implement automated responses for common incidents to reduce downtime and maintain service reliability.

### Input:
- A set of log files and performance metrics from multiple microservices.

### Output:
- A script or configuration for setting up monitoring, log analysis, and alerting using tools like Prometheus, Grafana, and ELK (Elasticsearch, Logstash, Kibana).
- A document outlining the incident response plan.

### Example:
Suppose you have three microservices: `service-A`, `service-B`, and `service-C`. Each service generates log files and metrics that need to be monitored.

1. **Service Metrics Collection**: Use Prometheus to scrape metrics from the services.
2. **Log Analysis**: Use ELK stack to analyze logs and detect anomalies.
3. **Alert Configuration**: Set up alerts in Prometheus and Grafana to notify the SRE team via email or Slack.
4. **Incident Response**: Create a script to restart a service if it crashes or to scale up resources if usage exceeds certain limits.

### Solution:

1. **Prometheus Configuration**:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'microservices'
    static_configs:
      - targets: ['service-A:9090', 'service-B:9090', 'service-C:9090']
```

2. **Grafana Dashboard**:
   - Create a dashboard in Grafana with panels for CPU usage, memory usage, response time, and error rate.
   - Configure alerts in Grafana for each metric.

3. **ELK Stack Configuration**:

**Logstash Configuration**:
```sh
input {
  file {
    path => "/var/log/service-A/*.log"
    start_position => "beginning"
  }
  file {
    path => "/var/log/service-B/*.log"
    start_position => "beginning"
  }
  file {
    path => "/var/log/service-C/*.log"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{TIMESTAMP_ISO8601:timestamp} %{LOGLEVEL:loglevel} %{GREEDYDATA:message}" }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "acme-logs-%{+YYYY.MM.dd}"
  }
  stdout { codec => rubydebug }
}
```

**Kibana**:
   - Create visualizations and dashboards for log levels, error rates, and response times.
   - Set up alerting in Kibana to notify the SRE team of anomalies.

4. **Incident Response Script** (example in bash):

```bash
#!/bin/bash

# Function to restart a service
restart_service() {
  local service_name=$1
  echo "Restarting $service_name..."
  systemctl restart $service_name
}

# Function to scale up resources
scale_up_resources() {
  local service_name=$1
  local current_instances=$(kubectl get deployment $service_name -o jsonpath='{.spec.replicas}')
  local new_instances=$((current_instances + 1))
  echo "Scaling up $service_name from $current_instances to $new_instances instances..."
  kubectl scale deployment $service_name --replicas=$new_instances
}

# Check CPU usage
cpu_usage=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
if (( $(echo "$cpu_usage > 80" | bc -l) )); then
  echo "High CPU usage detected: $cpu_usage%"
  restart_service "service-A"
  restart_service "service-B"
  restart_service "service-C"
fi

# Check memory usage
memory_usage=$(free | grep Mem | awk '{print $3/$2 * 100.0}')
if (( $(echo "$memory_usage > 75" | bc -l) )); then
  echo "High memory usage detected: $memory_usage%"
  scale_up_resources "service-A"
  scale_up_resources "service-B"
  scale_up_resources "service-C"
fi
```

### Submission:
Submit the following:
- `prometheus.yml` for Prometheus configuration.
- JSON or YAML files for Grafana dashboard and alerts.
- `logstash.conf` for Logstash configuration.
- A script file for incident response, named `incident_response.sh`.
- A document outlining the incident response plan, named `incident_response_plan.md`.
# aws-cloud-monitoring-dashboard
Automated AWS infrastructure monitoring and real-time alerting system using CloudWatch and SNS
# AWS Cloud Monitoring and Alerting Dashboard

## 📌 Project Overview
This project demonstrates how to set up a proactive infrastructure monitoring and automated alerting system within Amazon Web Services (AWS). By utilizing native cloud services, the architecture automatically tracks system performance thresholds and dispatches real-time incident notifications to administrators when anomalies occur, reducing the Mean Time to Detection (MTTD).

## 🗺️ Architecture Diagram
```text
  ┌─────────────────────────────────────────────────────────────┐
  │                        AWS CLOUD                            │
  │                                                             │
  │   ┌──────────────┐      Metrics       ┌───────────────┐     │
  │   │  Amazon EC2  │ ────────────────>  │  CloudWatch   │     │
  │   │  (Instance)  │                    │   (Alarms)    │     │
  │   └──────────────┘                    └───────┬───────┘     │
  │                                               │             │
  │                                               │ Breach      │
  │                                               ▼ Trigger     │
  │                                       ┌───────────────┐     │
  │                                       │  Amazon SNS   │     │
  │                                       │   (Topics)    │     │
  │                                       └───────┬───────┘     │
  └───────────────────────────────────────────────┼─────────────┘
                                                  │
                                                  │ Email Alert
                                                  ▼
                                         ┌─────────────────┐
                                         │  Administrator  │
                                         │    (Inbox)      │
                                         └─────────────────┘
```

## 🛠️ AWS Services Used
* **Amazon EC2:** Hosted the simulated enterprise application workload.
* **Amazon CloudWatch:** Configured custom metric tracking and static alarm threshold triggers (>80% CPU utilization).
* **Amazon SNS (Simple Notification Service):** Managed decoupled communication topics to route automated alerts to subscriber endpoints.

## 🚀 Implementation & Testing Steps
1. **Created SNS Alerting Engine:** Provisioned a standard SNS topic and subscribed an administrative email endpoint to receive JSON payloads.
2. **Launched EC2 Workload:** Deployed an Amazon Linux 2023 instance representing core infrastructure.
3. **Established CloudWatch Alarm:** Mapped an alarm monitoring the `CPUUtilization` metric on a 5-minute sampling interval with a static threshold of 80%.
4. **Executed Stress Test Simulation:** Connected to the EC2 instance via SSH and deployed the Linux `stress` utility (`sudo stress --cpu 1 --timeout 400s`) to force hardware utilization to 100%.

## 📊 Project Evidence & Metrics

### 1. CloudWatch Breach Detection
*Below is the live execution graph showing the blue metric line spiking past the 80% red threshold line during the simulation:*
![CloudWatch Graph](graph-screenshot.png)

### 2. Automated SNS Email Alert Received
*The automated email alert triggered instantly by Amazon SNS when the instance state shifted from `OK` to `ALARM`:*
![Email Alert](email-alert.png)

## 💡 Key Learnings
* Architecting cloud monitoring baselines and establishing system observability.
* Configuring automated incident alerting to minimize operational downtime.
* Simulating production infrastructure workloads using Linux stress utilities.

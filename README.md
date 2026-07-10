# Elastic SIEM Home Lab

A hands-on home lab demonstrating end-to-end SIEM operations: forwarding logs from a Kali Linux VM to Elastic Cloud, detecting simulated attacker activity in real time, and building dashboards/alerts in Kibana.

![Kibana Dashboard](docs/images/dashboard-overview.png)
*Replace with a screenshot of your main Kibana dashboard*

## Summary

This lab simulates a small-scale SOC monitoring pipeline. A Kali Linux VM generates system and network activity, Elastic Agent forwards logs to Elastic Cloud, and Kibana is used to detect and visualize security events — including live Nmap scan detection — in near real-time.

**Stack:** Elastic Agent · Elasticsearch · Kibana · Elastic Cloud · Kali Linux · Nmap · Bash

## Architecture

```
Kali Linux VM  --->  Elastic Agent  --->  Elastic Cloud (Elasticsearch)  --->  Kibana
   (target/                (forwards            (indices +                  (dashboards,
   log source)           logs securely)          storage)                    detection rules,
                                                                              alerts)
```

![Architecture Diagram](docs/images/architecture.png)
*Replace with a simple diagram of the flow above — even a hand-drawn one photographed works*

## What This Demonstrates

- **Log collection & forwarding** — configuring Elastic Agent on a Linux endpoint and securely transporting logs to a cloud-hosted Elasticsearch instance
- **Detection engineering** — building and tuning detection rules so that Nmap scanning activity is reliably flagged with minimal false positives
- **Real-time alerting** — Kibana alerts triggered by live events, not just historical queries
- **Dashboarding** — turning raw log data into an at-a-glance view of security-relevant activity
- **Troubleshooting** — diagnosing and resolving ingestion delays and configuration mismatches during setup

## Walkthrough

### 1. Elastic Agent Setup
Installed and enrolled Elastic Agent on the Kali Linux VM, configured to ship logs to an Elastic Cloud deployment over a secure connection.

![Agent Configuration](docs/images/agent-config.png)
*Replace with a screenshot of the agent enrollment/config screen*

### 2. Generating Security Events
Used Nmap to run scans against the monitored VM, producing network activity that the SIEM could detect and classify — a lightweight stand-in for real reconnaissance behavior.

![Nmap Scan](docs/images/nmap-scan.png)
*Replace with a screenshot of the scan and the corresponding detected event*

### 3. Detection & Alerting
Built detection rules in Kibana and tuned thresholds to reduce false positives while still catching scan activity in real time.

![Alert Fired](docs/images/alert-triggered.png)
*Replace with a screenshot of the alert firing in Kibana*

### 4. Dashboards
Created dashboards to visualize event volume, source/destination activity, and alert history for quick situational awareness.

## Challenges & Fixes

| Issue | Resolution |
|---|---|
| Log ingestion delays | Adjusted agent polling/output configuration to reduce lag between event and indexing |
| Noisy detection thresholds | Tuned rule conditions to cut false positives while keeping true positives |
| Secure transport misconfiguration | Corrected TLS/output settings between Elastic Agent and Elastic Cloud |

## Future Enhancements

- [ ] Integrate Suricata or Snort for network-layer (IDS/IPS) detection
- [ ] Containerize the lab setup with Docker for faster, repeatable deployment
- [ ] Expand to multiple endpoints/data sources for a more realistic enterprise scenario

## Docs

Full write-up, proposal, and progress reports are available in [`/docs`](./docs) for anyone who wants the detailed history of the project.

---

*Built as a self-directed learning project to bridge coursework in networking/security with practical SIEM operations.*

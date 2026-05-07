# Splunk-SOC-Detection-and-Incident-Workflow-Lab

## Overview

Built a SOC-focused detection and incident investigation lab using Splunk Enterprise and the BOTS v3 dataset to simulate real-world Tier 1 SOC analyst workflows. The lab focused on identifying indicators of compromise (IOCs), investigating suspicious authentication and web traffic activity, analyzing anomalous user behavior, and documenting incident-response recommendations through structured threat hunting and alert triage processes.

This project simulated how SOC analysts investigate potential threats, validate suspicious activity, reduce false positives, and escalate incidents based on severity and operational impact.

---

# Objectives

- Investigate suspicious authentication activity
- Identify indicators of compromise (IOCs)
- Perform threat hunting using SPL
- Analyze suspicious web traffic patterns
- Investigate abnormal 404 spikes and endpoint enumeration
- Detect anomalous user-agent behavior
- Simulate SOC alert triage workflows
- Document escalation and response recommendations
- Differentiate malicious behavior from false positives

---

# Environment

## Technologies Used

- Splunk Enterprise
- Splunk SPL
- BOTS v3 Dataset
- Windows Event Logs
- Web Traffic Logs
- Authentication Logs

---

# Dataset

## BOTS v3 Dataset

The BOTS v3 dataset was used to simulate enterprise log ingestion and SOC investigations. The dataset included:

- Windows authentication logs
- Web server traffic
- Endpoint telemetry
- User activity logs
- Suspicious authentication attempts
- HTTP request logs
- User-agent data

---

# Threat Scenarios Investigated

## 1. Failed Authentication Investigation

Investigated repeated failed login attempts to identify suspicious authentication activity and potential brute-force behavior.

### SPL Query

```spl
index=* EventCode=4625
| stats count by Account_Name, src_ip
| sort -count
```

### Investigation Focus

- Repeated failed logins
- High-volume authentication attempts
- Suspicious source IP addresses
- User targeting patterns

---

# 2. Failed → Successful Login Correlation

Investigated whether repeated failed logins eventually resulted in successful authentication activity.

### SPL Query

```spl
index=* (EventCode=4624 OR EventCode=4625)
| stats count by src_ip, EventCode
```

### Investigation Focus

- Potential credential compromise
- Brute-force success indicators
- Authentication sequence analysis
- Lateral movement risk identification

---

# 3. 404 Spike Investigation

Analyzed spikes in HTTP 404 responses to identify possible endpoint enumeration or scanning behavior.

### SPL Query

```spl
index=* status=404
| timechart count by uri_path
```

### Findings

Observed repeated requests against suspicious endpoints including:

- /member.php
- /robots.txt
- /favicon.ico

This activity simulated reconnaissance and endpoint enumeration behavior commonly observed during early attack phases.

---

# 4. Suspicious Endpoint Analysis

Investigated abnormal endpoint access behavior and repetitive URI requests.

### SPL Query

```spl
index=* uri_path=*
| stats count by uri_path
| sort -count
```

### Investigation Focus

- Enumeration activity
- High-frequency endpoint requests
- Reconnaissance behavior
- Web application probing

---

# 5. User-Agent Anomaly Investigation

Analyzed user-agent strings to identify unusual or suspicious traffic patterns.

### SPL Query

```spl
index=* user_agent=*
| stats count by user_agent
| sort -count
```

### Investigation Focus

- Automated tooling indicators
- Scripted request behavior
- Scanner activity
- Abnormal client behavior

---

# IOC Investigation Workflow

## Indicators Investigated

- Suspicious source IP addresses
- Failed authentication spikes
- Repeated endpoint enumeration
- Abnormal web requests
- Unusual user-agent behavior
- High-frequency authentication attempts

---

# Alert Triage Workflow

## Triage Process

### Step 1 — Alert Validation

- Verified suspicious activity
- Confirmed event legitimacy
- Reviewed affected systems

### Step 2 — Investigation

- Correlated related events
- Identified source IP behavior
- Investigated authentication activity
- Reviewed endpoint access patterns

### Step 3 — Severity Assessment

Classified alerts based on:

- Authentication volume
- Endpoint targeting
- IOC presence
- Potential compromise indicators

### Step 4 — Escalation Decision

Escalated incidents if:

- Failed logins correlated with successful access
- Multiple systems were targeted
- Enumeration activity increased
- Additional suspicious behavior was identified

---

# False Positive Analysis

Not all suspicious events were treated as malicious activity.

## Potential False Positives

- Users forgetting passwords
- VPN reconnect attempts
- Automated internal scanners
- Legitimate search engine crawlers
- Service account authentication failures

This analysis simulated realistic SOC decision-making and operational triage processes.

---

# Response Recommendations

## Recommended Actions

- Block malicious IP addresses
- Reset affected credentials
- Enable MFA enforcement
- Investigate lateral movement
- Review additional host activity
- Monitor authentication patterns
- Increase alerting thresholds for suspicious activity

---

# MITRE ATT&CK Mapping

## Techniques Identified

| Technique | Description |
|---|---|
| T1110 | Brute Force |
| T1078 | Valid Accounts |
| T1021 | Remote Services |
| T1595 | Active Scanning |

---

# Investigation Findings

## Key Findings

- Identified repeated failed authentication attempts from suspicious IP addresses
- Observed endpoint enumeration behavior through repeated URI requests
- Investigated abnormal 404 traffic spikes
- Correlated suspicious authentication activity with potential compromise indicators
- Performed IOC-focused threat hunting across multiple log sources
- Simulated Tier 1 SOC investigation and escalation workflows

---

# Skills Demonstrated

- Splunk SPL
- Threat hunting
- IOC analysis
- SOC triage workflows
- Authentication investigations
- Web traffic analysis
- Incident investigation
- Detection analysis
- False positive reduction
- MITRE ATT&CK mapping

---

# Screenshots

## Suggested Screenshot Names

```text
01_failed_authentication_analysis.png
02_top_source_ips.png
03_failed_successful_correlation.png
04_404_spike_analysis.png
05_endpoint_enumeration.png
06_user_agent_analysis.png
07_alert_triage_workflow.png
08_mitre_mapping.png
09_response_recommendations.png
```

---

# Resume Bullet

- Built a Splunk SOC detection and incident workflow lab using the BOTS v3 dataset to investigate authentication threats, analyze suspicious web traffic, perform IOC-based threat hunting, and simulate Tier 1 SOC alert triage and escalation workflows.

---

# Lessons Learned

- Effective SOC investigations require correlation across multiple log sources
- Authentication failures alone are not always malicious
- False positive analysis is critical during triage
- Web traffic anomalies can indicate reconnaissance activity
- IOC investigations improve detection accuracy
- Structured incident workflows improve operational response efficiency

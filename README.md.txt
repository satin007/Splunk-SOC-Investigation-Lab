# Splunk SOC Investigation & Detection Lab

## Overview

This project demonstrates a beginner-level Security Operations Center (SOC) investigation using Splunk Enterprise and a tutorial log dataset. The objective was to analyze SSH authentication failures, identify suspicious source IP addresses, examine targeted usernames, and create a monitoring dashboard.

## Objectives

- Search and filter SSH authentication logs using SPL.
- Identify source IPs generating high volumes of failed password attempts.
- Extract usernames and source IP addresses using `rex`.
- Count failed attempts and distinct usernames using `stats` and `dc()`.
- Check for matching successful password logins.
- Visualize SSH activity in a Splunk dashboard.
- Document findings and recommended SOC response actions.

## Lab Environment

- **SIEM:** Splunk Enterprise
- **Dataset:** `tutorialdata.zip`
- **Host field:** `vyom`
- **Sourcetype:** `www1/secure`
- **Platform:** Windows 11 local lab

## Investigation Findings

| Source IP | Failed attempts | Unique usernames | Matching successful password logins found |
|---|---:|---:|---:|
| `87.194.216.51` | 948 | 140 | 0 |
| `211.166.11.101` | 743 | 135 | 0 |

Both IPs generated patterns consistent with SSH password guessing or username enumeration. No matching successful password-login events were found for these IPs in the searched dataset.

These findings are based on the available tutorial logs and do not prove that all access methods failed or establish malicious intent by themselves.

## Detection Approach

The detection query groups failed SSH password events by source IP and identifies IPs with at least 20 failed attempts and at least 10 unique usernames.

The thresholds are initial lab values, not universal production settings.

## Dashboard

The `SSH Threat Monitoring Dashboard` contains:

1. Top Failed SSH Source IPs
2. Failed SSH Attempts Over Time
3. Total Failed SSH Attempts
4. Top Targeted SSH Usernames

## Tools and Techniques

- Splunk Search & Reporting
- SPL filtering, aggregation, and sorting
- Regular expression field extraction with `rex`
- Distinct-value counting with `dc()`
- Time-series analysis with `timechart`
- Authentication log analysis
- Dashboard visualization and incident documentation

## Repository Structure

```text
Splunk-SOC-Investigation-Lab/
├── README.md
├── screenshots/
├── investigation/
│   └── ssh-investigation-report.md
├── detections/
└── dashboard/
```

## Limitations

This is a local learning project using tutorial data, not a live production SOC. Detection thresholds would need validation and tuning against the environment in which they are deployed.

## Learning Outcome

Practiced a basic SOC workflow: search authentication logs, identify suspicious patterns, investigate source IPs and usernames, check for matching successful logins, visualize findings, and document evidence-based recommendations.

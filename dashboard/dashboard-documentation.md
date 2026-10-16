# SSH Threat Monitoring Dashboard

## Overview

The SSH Threat Monitoring Dashboard was created in Splunk Enterprise using the `tutorialdata.zip` dataset. It summarizes failed SSH password authentication activity to support initial SOC investigation.

## Dashboard Panels

### 1. Top Failed SSH Source IPs
Ranks source IP addresses by the number of failed SSH password events. Helps identify the most active sources.

### 2. Failed SSH Attempts Over Time
Displays failed SSH password events over time using a daily time chart. Helps identify changes or spikes in activity.

### 3. Total Failed SSH Attempts
Shows the total number of matching failed SSH password events in the selected time range.

### 4. Top Targeted SSH Usernames
Ranks attempted usernames by the number of failed SSH password events. Helps identify frequently targeted accounts.

## Dataset and Search Context

- Dataset: `tutorialdata.zip`
- Host: `vyom`
- Sourcetype: `www1/secure`
- Time range used for analysis: All time

## Analyst Use

A SOC analyst can use these panels to identify suspicious source IPs, examine authentication activity over time, and prioritize usernames for further investigation.

## Limitations

This is a local learning lab using tutorial data, not live production monitoring. Dashboard results depend on the available events and the selected time range.

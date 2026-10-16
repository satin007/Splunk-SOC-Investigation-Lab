# SSH Brute-Force Investigation Report

## 1. Objective

Investigate failed SSH password authentication events in Splunk to identify suspicious source IP addresses, examine targeted usernames, and check for matching successful password logins.

## 2. Environment

- SIEM: Splunk Enterprise
- Dataset: Splunk tutorial dataset (`tutorialdata.zip`)
- Log sourcetype: `www1/secure`
- Search host: `vyom`
- Investigation type: SSH authentication activity analysis

## 3. Detection Logic

The detection query extracted source IP addresses and attempted usernames from failed SSH password events. It grouped events by source IP and highlighted IPs meeting both of these lab thresholds:

- At least 20 failed password attempts
- At least 10 unique usernames attempted

These are initial lab thresholds and would require tuning in a real environment.

## 4. Findings

| Source IP | Failed attempts | Unique usernames | Matching successful password logins |
|---|---:|---:|---:|
| 87.194.216.51 | 948 | 140 | 0 |
| 211.166.11.101 | 743 | 135 | 0 |

The second IP's most frequently attempted usernames included `root` (29 attempts), `operator` (26), and `admin` (21).

## 5. Analysis

Both IP addresses generated high volumes of failed SSH password events across many usernames. This pattern is consistent with automated password guessing or username enumeration.

The searches found no matching successful password-login events for either IP in the investigated dataset. This does not prove that every possible access method failed.

## 6. Recommended SOC Response

1. Review the full authentication timeline and relevant surrounding events.
2. Check whether either source IP is expected or authorized.
3. Correlate with successful logins, other authentication methods, and endpoint telemetry.
4. If this were a live environment and the activity were confirmed malicious, follow the organization's incident response process to block or restrict the source where appropriate.
5. Tune detection thresholds to reduce false positives and validate alert behavior.

## 7. Limitations

This investigation uses a local tutorial dataset rather than live production telemetry. The findings are based on the available events and the selected search conditions.

## 8. Tools and Skills

- Splunk Search & Reporting
- SPL filtering and aggregation
- Field extraction with `rex`
- Distinct-value counting with `dc()`
- Time-series analysis with `timechart`
- Authentication log investigation
- Basic detection logic and dashboard visualization

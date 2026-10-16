# SSH Password Guessing Detection

## Objective

Identify source IP addresses generating high volumes of failed SSH password attempts across multiple usernames.

## SPL Query

```spl
source="tutorialdata.zip:*" host="vyom" sourcetype="www1/secure" "Failed password"
| rex field=_raw "Failed password for (?:invalid user )?(?<username>\S+) from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count as failed_attempts dc(username) as unique_usernames by src_ip
| where failed_attempts >= 20 AND unique_usernames >= 10
| sort - failed_attempts
```

## Detection Logic

- `rex` extracts the attempted username and source IP from each matching log event.
- `stats count` counts failed password events per source IP.
- `dc(username)` counts the distinct usernames attempted.
- `where` flags IPs with at least 20 failed attempts and 10 or more unique usernames.
- `sort` ranks the results by failed attempts, highest first.

## Lab Results

| Source IP | Failed attempts | Unique usernames |
|---|---:|---:|
| 87.194.216.51 | 948 | 140 |
| 211.166.11.101 | 743 | 135 |

## Analyst Interpretation

Both IPs exhibit patterns consistent with SSH password guessing or username enumeration. These results are indicators for investigation, not definitive proof of malicious activity.

## Limitations

The thresholds are initial lab values and should be tuned and tested before use in a production environment. Results depend on the available dataset and selected time range.

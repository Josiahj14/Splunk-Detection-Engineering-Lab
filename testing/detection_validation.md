# Detection Validation Results

## Test Environment
Platform: Splunk Cloud Platform
Index: security_lab
Data: Synthetic authentication and Windows security events

## Detection 1: Brute Force

Objective:
Detect 5 failed logins from one IP within 10 minutes.

Positive Test: PASS
- 192.0.2.10 detected.
- 203.0.113.50 detected.
- Both met 5-failure threshold

Negative Test: PASS
- Simulated failed logins spread across 20 minutes
- Duplicate ingested test events were removed for validation.
- Detection returned no matches.

## Detection 2: Password Spraying

Objective:
Detect at least 5 failed logins against 5 unique users within 10 minutes.

Positive Test: PASS
- Source IP: 198.51.100.44
- Failed logins: 5
- Unique users: 5

Negative Test: Not yet performed.

## Detection 3: Windows Privilege Changes

Objective:
Detect a newly created account added to Administrators within 10 minutes.

Positive Test: PASS
- Account: newadmin
- Time difference: 60 seconds

Negative Test: PASS
- Simulated a 780-second delay.
- Detection returned no matches.

Correlation Tuning: PASS
- Identified a false-negative scenario caused by selecting the earliest account creation event.
- Original calculation: 4080 seconds.
- Updated the detection to track the most recent preceding account creation.
- Corrected calculation: 60 seconds.

## Scheduled Alert

Configuration: Completed
- Scheduled daily at 6:00 AM.
- Trigger condition: Results greater than 0.
- Severity: Medium.

Acutal scheduled trigger: Not yet verified.

## Limitations

- Testing used synethic security events.
- Detection rule require additional production tuning.
- Scheduled alert execution still requires validation.
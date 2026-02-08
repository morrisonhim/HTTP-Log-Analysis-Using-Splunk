# HTTP-Log-Analysis-Using-Splunk
# Project Overview
This project demonstrates a practical, hands-on approach to analyzing HTTP web server logs using Splunk. The objective was to ingest a pre-existing Apache access log, extract meaningful fields, identify suspicious or anomalous activity, and generate actionable security insights. The project simulates real-world log analysis scenarios such as detecting brute-force attempts, suspicious HTTP methods, error spikes, and malicious user agents.

**Objectives**
- Ingest and index HTTP access logs into Splunk
- Understand HTTP log formats and extracted fields
- Perform structured searches using SPL(Search Processing Language)
- Detect suspicious behavior and potential web attacks

**Lab Environment**
- Platform: Splunk Enterprise
- Log Source: Pre-existing Apache HTTP access log
- Operating System: Ubuntu Server 25.10

**Step 1: Log Ingestion into Splunk**
1. Logged into Splunk Web
2. Navigated to Settings → Add Data
3. Selected Upload
4. Uploaded the pre-existing HTTP access log file
5. Configured:
- Source Type: ```access_combined```
- Index: ```main```
6. Reviewed field extraction
7. Submitted data for indexing

**Step 2: Verifying Successful Ingestion**



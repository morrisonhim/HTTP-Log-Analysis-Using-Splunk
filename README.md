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
- Verified successful ingestion: ```index:main```
**Verification checks:**
- Events visible in Splunk
- Correct timestamp parsing
- Automatic field extraction (clientip, method, uri, status)
![successful ingestion](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/successful%20ingestion.png)

**Step 3: Basic Traffic Analysis**
- Searched for Total HTTP Requests: ```index=web_logs | stats count```
![basic traffic analysis](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/basic%20traffic%20analysis.png)

- Searched for Requests per IP Address: ```index=main | stats count by clientip | sort -count```
![requests per ip address](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/requests%20per%20ip%20address.png)
  





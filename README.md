# HTTP-Log-Analysis-Using-Splunk
# Project Overview
This project demonstrates a hands-on analysis of HTTP web server logs using Splunk to extract meaningful insights related to web traffic behavior, performance monitoring, and security detection. The analysis simulates real-world scenarios such as identifying suspicious IP activity, abnormal HTTP methods, error spikes, and potentially malicious user agents.
The project emphasizes practical SIEM skills, log parsing, SPL querying, and security-oriented thinking.

# Objectives
- Ingest and index HTTP access logs into Splunk
- Understand HTTP log formats and extracted fields
- Perform structured searches using SPL(Search Processing Language)
- Detect suspicious behavior and potential web attacks

# Lab Environment
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
Purpose: Identify high-volume IPs and potential scanning behavior.

**Step 4: HTTP Method Analysis**
- Spl: ```index=main | stats count by method```
![method analysis](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/method%20analysis.png)

**Step 5: HTTP Status Code Analysis**
- Spl: ```index=main | stats count by status```
![status code analysis](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/status%20code%20analysis.png)
**Key Indicators:**
- 200 – Successful requests
- 206 - Partial Content - Used for downloads
- 301 - Moved Permanently – URL redirect (often HTTP → HTTPS)
- 304 - Not Modified – Cached content used
- 401 / 403 – Unauthorized access attempts
- 404 – Resource enumeration
- 416 - Range Not Satisfiable
- 500 – Server-side errors

**Step 6: Suspicious User-Agent Analysis**
- Spl: ```index=main
| stats count by useragent
| sort -count```
![suspicious user-agent analysis](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/suspicious%20user-agent%20analysis.png)
- Flagged Indicators:
- ```curl```
- ```python-requests```
- Automated or empty user-agent strings

**Step 7: Web Scanning Detection**
- Spl: ```index=main
| stats dc(uri) as unique_uris by clientip
| where unique_uris > 50```
![web scanning detection](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/web%20scanning%20detection.png)
High URI diversity from a single IP suggests automated scanning.

**Step 8: Time-Based Analysis**
- Spl: ```index=main
| timechart count by status```
![time-based analysis](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/time-based%20analysis.png)

**Step 9: Successful vs Error Responses**
- Spl: ```index=web_logs
| eval response_type=case(
    status>=200 AND status<300,"Success",
    status>=300 AND status<400,"Redirection",
    status>=400 AND status<500,"Client Error",
    status>=500,"Server Error"
)
| stats count by response_type```
![successful vs errors](https://github.com/morrisonhim/HTTP-Log-Analysis-Using-Splunk/blob/main/successful%20vs%20errors.png)

# Findings & Observations
- Detected repeated 401, 403, and 404 responses indicating unauthorized access and resource enumeration.
- Observed suspicious user agents (curl, python-requests, empty UA) linked to scripted activity.
- Several IP addresses accessed an unusually high number of unique URIs, strongly indicating automated web scanning or enumeration activity.
- Time-based analysis revealed short bursts of high traffic and error responses, inconsistent with normal user behavior and indicative of possible attack activity
- Overall findings demonstrate how Splunk enables effective detection of anomalous web activity and supports proactive web security monitoring.

## Conclusion
This project showcases the practical use of Splunk for HTTP log analysis and web security monitoring. The
techniques demonstrated are directly applicable to real-world SOC environments and highlight the
importance of log analysis in detecting and responding to web-based attacks.







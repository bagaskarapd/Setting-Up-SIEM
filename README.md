<h1>Project: Setting Up a SIEM for Threat Detection</h1>
<p>
  As an Informatics Engineering graduate aspiring to become a Security Operations Center (SOC) Analyst, I created this project to demonstrate my ability to deploy and utilize a Security Information and Event Management (SIEM) solution. This hands-on lab walks through the process of setting up Splunk to monitor, analyze, and detect security threats in real-time.
</p>
<h2>Objective</h2>
<ul>
  <li>install and configure Splunk</li>
  <li>collect security logs from systems and analyze real-time threats</li>
  <li>create alerts for suspicious activity (failed logins, brute-force attempts, unusual network behavior)</li>
</ul>

<h3>Tools Used</h3>
<ul>
  <li><strong>Splunk</strong></li>
  <li><strong>Virtual Machine(Windows10pro)</strong></li>
<hr />

<h2>Step 1: Choosing SIEM Tool</h2>
<p>There are several SIEMs out there, but i focus on Splunk (free version) for this lab.
  Splunk is a powerful and widely used SIEM tool. I used the Free Edition, which is sufficient for lab and training purposes.
</p>
<a href="https://www.linkedin.com/in/ananda-bagaskara-poetra-dwiki-34492b221/](https://www.splunk.com/en_us/download.html">
  <img src="https://img.shields.io/badge/-Splunk-000000?&style=for-the-badge&logo=Splunk&logoColor=white" />
</a>

<h2>Step 2: Install and Configure Splunk</h2>
<ul>
  <li>Installing Splunk on local machine or a virtual machine (VM).</li>
  <li>Open Splunk Web Interface (Default: http://localhost:8000).</li>
  <li>Create an admin account and log in.</li>
  <li>Adding first data source: Windows Event Logs or Linux Syslogs.</li>
</ul>

<h2>Step 3: Collect and Analyze Security Logs</h2>
<p>
  Once logs were collected, I performed analysis using SPL (Search Processing Language).
</p>
<h4>Example Query: Detect Failed Login Attempts</h4>
<pre>
index=_internal sourcetype=auth.log | stats count by user, source_ip
</pre>
<p>This query shows failed login attempts per user and IP. Useful for detecting brute-force behavior.</p>

<h2>Step 4: Create Real-Time Alert</h2>
<p>
  I created an alert to simulate how SOC teams monitor and respond to active threats.
</p>
<ul>
  <li><strong>Goal:</strong> Trigger an alert when there are 5 or more failed login attempts within 1 minute</li>
  <li>Navigate to <code>Search & Reporting</code>, enter this query:
    <pre>
index=_internal sourcetype=auth.log action=failed 
| stats count by user, source_ip 
| where count >= 5
    </pre>
  </li>
  <li>Save it as a Real-Time Alert</li>
  <li>Set up email or script-based notifications</li>
</ul>
<hr />


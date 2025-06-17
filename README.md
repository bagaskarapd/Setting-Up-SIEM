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
  <li><strong>Virtual Box(Windows10pro)</strong></li>
<hr />
 <p align="center">
    <img src="https://github.com/bagaskarapd/Setting-Up-SIEM/blob/main/Screenshots/Setting-Up-SIEM.png?raw=true">
</p>
  

<h2>Step 1: Choosing SIEM Tool</h2>
<p align="center">
    <img src="https://github.com/bagaskarapd/Setting-Up-SIEM/blob/main/Screenshots/Splunk.png?raw=true">
</p>
<p>There are several SIEMs out there, but i focus on Splunk (free version) for this lab.
  Splunk is a powerful and widely used SIEM tool. I used the Free Edition, which is sufficient for lab and training purposes.
</p>
<a href="https://www.splunk.com/en_us/download.html">
  <img src="https://img.shields.io/badge/-Splunk-000000?&style=for-the-badge&logo=Splunk&logoColor=white" />
</a>

<h2>Step 2: Install and Configure Splunk</h2>
<p>To begin this project, I installed Splunk Enterprise (Free Edition) on a Windows 10 Pro virtual machine that I set up using VirtualBox. I chose a virtual machine so I could safely experiment and simulate security monitoring without affecting my main system. Once the installation was complete, I accessed the Splunk Web interface through the browser at <code>http://localhost:8000</code>. I created an admin account during the initial setup, which gave me access to the full dashboard and configuration settings. This step was essential because it allowed me to build a controlled environment where I could test real SIEM use cases.</p>

<h3>Creating a Custom Index (win_logs)</h3>
<p>Before collecting logs, I created a custom index named <code>win_logs</code> via the Splunk settings under <strong>Settings → Indexes → New Index</strong>. Creating a separate index helped me keep the Windows logs organized and made it easier to run focused search queries. Instead of storing all logs in the default <code>main</code> index, using <code>win_logs</code> allowed me to isolate system event data and simulate how logs would be categorized in a production environment.</p>
<p align="center">
  <img src="">
</p>

<h2>Step 3: Collect and Analyze Security Logs</h2>
<p align="center">
    <img src="https://github.com/bagaskarapd/Setting-Up-SIEM/blob/main/Screenshots/Analyzing%20Failed%20Login%20Attempts.png?raw=true">
</p>
<p>I then proceeded to add a data source by going to <strong>Settings → Add Data → Monitor → Local Event Logs</strong>. From there, I selected the <strong>Security</strong> log, which includes critical Windows Event IDs like <code>4624</code> for successful logins and <code>4625</code> for failed login attempts. I assigned this data source to the <code>win_logs</code> index I had created earlier. By collecting Security logs specifically, I could monitor authentication-related activities and gain insight into who was trying to access the system and whether any access attempts were suspicious.</p>
<p align="center">
  <img src="https://github.com/bagaskarapd/Setting-Up-SIEM/blob/main/Screenshots/Event%20Log%20Collections.png?raw=true">
</p>
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


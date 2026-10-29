# Building-an-Automated-Email-Phishing-Detection-System
building an automated email phishing detection system with an integrated AI Agent using Wazuh, Gmail IMAP, Oracle cloud, a python-based scanner that runs on a schedule using cron. The system analyzes emails for multiple Phishing indicators, generates alerts and summaries directly in the Wazuh Dashboard. 


<table>
  <tr>
    <th>Component</th>
    <th>Details</th>
  </tr>
  <tr>
    <td>Cloud</td>
    <td>Oracle Cloud, Region - Johannesburg</td>
  </tr>
  <tr>
    <td>Manager VM</td>
    <td>Ubuntu 22.04, 2 OCPU, 12 GB RAM, wazuh 4.14 all-in-one (manger, indexer, dashboard)</td>
  </tr>
  <tr>
    <td>Agent VM</td>
    <td>Ubuntu 22.04, 1 OCPU, Wazuh agent 4.14, python 3 venv, cron</td>
  </tr>
  <tr>
    <td>Mail</td>
    <td>Throwaway Gmail account(s), IMAP + app password(2-step verification on)</td>
  </tr>
  <tr>
    <td>AI</td>
    <td>Gemini API, Flash-Lite class model</td>
  </tr>
</table>

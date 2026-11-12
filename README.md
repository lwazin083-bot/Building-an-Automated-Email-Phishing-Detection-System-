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
<br/>
<br/>
<p align="center">
In Oracle cloud we set up our Manager Virtual Machine -- Ubuntu 22.04, 2 OCPU, 12 GB RAM. <br>
<img src="https://i.imgur.com/WyVGyeW.png" height="80%" width="80%"/>
<br />
<img src="https://i.imgur.com/GlS2yNa.png" height="80%" width="80%"/>
<br/>
<br/>
Set up public IPv4 address:
<img src="https://i.imgur.com/16QiYlu.png" height="80%" width="80%"/>
<br/>
<br/>
On the terminal we connect to the VM over SSH using the SSH keys we saved when creating the VM:
<img src="https://i.imgur.com/zKEnnoz.png" height="80%" width="80%"/>
<br/>
<br/>
We then install Wazuh 4.14 on the VM. <br/>
<i>curl -s0 https://packages.wazuh.com/4.14/wazuh-install.sh</i>
<br/>
<i>sudo bash wazuh-install.sh -a 2>&1 | tee ~/wazuh-install.log</i><br/>
<img src="https://i.imgur.com/Tgy3AYH.png" height="80%" width="80%"/>
<br/>
<br/>
Open port 443 in Oracle's firewall.<br/>
Add Ingress rules: <br/>
Rule 1 (dashboard): <br/>
<img src="https://i.imgur.com/baWTaxN.png" height="80%" width="80%"/>
<br/>
Rulr 2 (agents): <br/>
<img src="https://i.imgur.com/o4clmym.png" height="80%" width="80%"/>
<br/> 
<br/>
Opening the dashboard. <br/>
<img src="https://i.imgur.com/MDoIfoE.png" height="80%" width="80%"/>









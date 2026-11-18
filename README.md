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
Opening the Wazuh dashboard. <br/>
<img src="https://i.imgur.com/MDoIfoE.png" height="80%" width="80%"/>
<br/>
<br/>
Create the agent VM. <br/>
<img src="https://i.imgur.com/V8e2t8T.png" height="80%" width="80%"/>
<br/>
<br/>
On the terminal we connect to the agent VM. <br/>
<img src="https://i.imgur.com/otxZqjN.png" height="80%" width="80%"/>
<br/>
<br/>
Install the Wazuh agent on the agent VM. <br/>
<img src="https://i.imgur.com/jQrnjEu.png" height="80%" width="80%"/>
<br/>
<br/>
The agent has been installed and is active as seen on the Wazuh dashboard. <br/>
<img src="https://i.imgur.com/UtQOy63.png" height="80%" width="80%"/>
<br/>
<br/>
Install python tools on the agent VM. <br/>
<img src="https://i.imgur.com/NMGBgf9.png" height="80%" width="80%"/>
<br/>
<br/>
With the <i>sudo nano /etc/phishing_detector.env</i> command we will store Gmail credentials so that our script can read the emails from a protected file. <br/>
We then load the python script and do a test run and we can see that the scanner works: <i>"Clean email scan complete: 11 new scanned, 0 flagged."</i> <br/>
<img src="https://i.imgur.com/fkTUDim.png" height="80%" width="80%"/>
<br/>
<br/>
Get the agent to watch the log file and then restart the VM <br/>
<img src="https://i.imgur.com/9CIHwqG.png" height="80%" width="80%"/>
<br/>
<br/>
Add custom rules on the Manager VM. <br/>
<img src="https://i.imgur.com/StXlgvO.png" height="80%" width="80%"/>
<br/>
<br/>
Validating that the pipeline works after sending a test phishing email to our throwaway email that is being watched by this system. <br/>
<img src="https://i.imgur.com/Aql9vvE.png" height="80%" width="80%"/>
<br/>
<img src="https://i.imgur.com/0dNsKjC.png" height="80%" width="80%"/>
<br/>
<br/>
Add a cron job on the agent VM that will automatically run the scanner on a schedule. <br/>
<img src="https://i.imgur.com/kTnLqcM.png" height="80%" width="80%"/>
<br/>
<br/>
The Phishing emails caught on our Wazuh SIEM under rule 100207. <br/>
<img src="https://i.imgur.com/Q8Lde67.png" height="80%" width="80%"/>
<br/>
<br/>
Now that our detection pipeline and our SIEM does get the telemtry, we will incorporate AI into the system -- Gemini API, Flash-Lite class model. <br/>
<img src="https://i.imgur.com/E0KoGJo.png" height="80%" width="80%"/>
<br/>
<br/>
Updated python script </br>
<img src="https://i.imgur.com/AIGiUyf.png" height="80%" width="80%"/>
<br/>
<br/>
Swap the new script under the same name as the old ones so the cron job does not need changing, then test it, and now the new lines are ending with "sent for AI review <br/>
<img src="https://i.imgur.com/wZXXAak.png" height="80%" width="80%"/>
<br/>
<br/>
Checking the candidate files "<i>cat /var/log/phishing_candiadate.jsol"</i> <br/>
<img src="https://i.imgur.com/nHsS2xb.png" height="80%" width="80%"/>
<br/>
<br/>
load the AI triage script, the script reads new record then asks Gemeni for a verdict.<br/> <br/>
<img src="https://i.imgur.com/lflR2WP.png" height="80%" width="80%"/>
<br/>
<br/>














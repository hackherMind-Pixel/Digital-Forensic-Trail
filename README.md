# Digital-Forensic-Trail
A mini-project that is on the look out of the chain of digital evidence left behind by actions on a system, network or a device that investigators can follow to reconstruct what happened. 
---

## 🔍 Phase 7: Log Analysis & Incident Response (The Detective)
In the final phase,my mission was to access the web server internal logs on the metasploitable machine to identify **Indicators of Compromise (IoC)** and the specific 'malicious string' used to get in.

### 1. Identifying the "Crime Scene"
I navigated to the Apache web server logs on the victim machine:
`cd /var/log/apache2`

### 2. Forensic Investigation
I used the command `trail -n 20 access.log` to hunt the attacker.
Since the log was huge I used the `grep` command, I filtered the `access.log` for malicious POST requests,this showed me how the Metasploit sent the 'Exploit code' to the server:
`grep "POST" access.log`
<img width="955" height="1044" alt="The Forensic" src="https://github.com/user-attachments/assets/7ad3dffd-6e70-4994-b8dd-800d13781001" />

### 3. Findings:
* **Attacker IP:** 192.168.56.102
* **Target:** `/index.php`
* **Exploit Payload:** Identified the injection of PHP configuration arguments. In other situations one might need to use (`allow_url_include=on`, `safe_mode=off`)  to bypass security filters.
* **HTTP Status Code:** The logs showed a **200 OK** response, confirming the payload was successfully accepted and executed by the server.

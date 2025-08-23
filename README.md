#  Web Security Lab  

A hands-on **Web Security Lab** showcasing both **defensive** and **offensive** approaches to securing web applications. This project simulates real-world attacks against vulnerable web apps (DVWA, OWASP Juice Shop) and defends them using industry-recognized tools like **pfSense** and **ModSecurity**.  

The lab is designed to demonstrate practical skills in **Web Application Security, Penetration Testing, and SOC Operations**, mapping scenarios to the **OWASP Top 10** and **MITRE ATT&CK framework**.  

---

##  Defensive Components  
- **pfSense Firewall Lab** – Network-level security with IDS/IPS (Snort/Suricata).  
- **ModSecurity Lab** – Open-source WAF configured to detect and block malicious HTTP requests.  

---

##  Offensive Components  
- **DVWA (Damn Vulnerable Web App)** – Classic vulnerable PHP app for learning OWASP Top 10.  
- **OWASP Juice Shop** – Modern vulnerable app with rich attack surfaces.  
- **Kali Linux Toolkit** – Attacks performed with industry tools:  
  - **OWASP ZAP** (Web app scanning & proxying)  
  - **Burp Suite Community** (Web vulnerability scanner)  
  - **SQLMap** (Automated SQL injection tool)  
  - **Nikto** (Web server scanner)  
  - **WPScan** (WordPress security scanner)  
  - **ClamAV** (Malware detection on files)  

---

##  Learning Outcomes  
- Configure and harden **firewalls (pfSense)** and **Web Application Firewalls (ModSecurity)**.  
- Perform **web penetration testing** using Kali Linux tools.  
- Simulate **attacks vs. defenses** to understand SOC workflows.  
- Map findings to **OWASP Top 10** and **MITRE ATT&CK** techniques.  

---

##  Future Enhancements  
- Integration with **Wazuh SIEM** for centralized log monitoring.  
- Automation of attack simulations for repeatable testing.  
- Custom ModSecurity rules for advanced protection scenarios.  

---

##  Note  
This lab is for **educational purposes only**. All experiments are performed in a controlled environment with intentionally vulnerable systems.  

---


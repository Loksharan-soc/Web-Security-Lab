# ModSecurity Installation on Ubuntu (WAF Lab)

## Overview
This guide walks through installing **ModSecurity** (Web Application Firewall) on **Ubuntu 22.04** with **Apache** and the **OWASP Core Rule Set (CRS)**. This WAF setup will protect backend web applications (e.g., DVWA or Juice Shop) from common attacks.

---

## Prerequisites
- Ubuntu 22.04 VM (WAF server)  
- Apache installed or no conflicting web server running  
- Basic knowledge of Linux commands

---

## Step 1: Update the System
```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2: Install Apache and ModSecurity
```bash
sudo apt install apache2 libapache2-mod-security2 modsecurity-crs -y
```

**Installed components:**
- `apache2` → Web server
- `libapache2-mod-security2` → ModSecurity module for Apache
- `modsecurity-crs` → OWASP Core Rule Set

---

## Step 3: Enable ModSecurity Module
```bash
sudo a2enmod security2
sudo systemctl restart apache2
sudo systemctl status apache2
```

---

## Step 4: Configure ModSecurity in Detection Mode
```bash
sudo cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
sudo nano /etc/modsecurity/modsecurity.conf
```

- Find the line:
```
SecRuleEngine DetectionOnly
```
- Keep it as `DetectionOnly` for now (logs attacks without blocking).  
- Later, you can change it to `SecRuleEngine On` to enable blocking.

---

## Step 5: Enable OWASP CRS
Ubuntu stores CRS in:

- Setup file: `/etc/modsecurity/crs/crs-setup.conf`  
- Rules directory: `/usr/share/modsecurity-crs/rules/`

Update Apache ModSecurity config:

```bash
sudo nano /etc/apache2/mods-enabled/security2.conf
```

Replace the content with:

```apache
<IfModule security2_module>
    # Persistent ModSecurity data
    SecDataDir /var/cache/modsecurity

    # Include all local ModSecurity config
    IncludeOptional /etc/modsecurity/*.conf

    # Include OWASP CRS
    IncludeOptional /etc/modsecurity/crs/crs-setup.conf
    IncludeOptional /usr/share/modsecurity-crs/rules/*.conf
</IfModule>
```

---

## Step 6: Restart Apache
```bash
sudo systemctl restart apache2
sudo systemctl status apache2
```

Check that Apache is **active (running)**.

---

## Step 7: Verify ModSecurity
Send a test request:

```bash
curl "http://localhost/?id=' OR '1'='1"
```

- In **DetectionOnly** → request succeeds, but ModSecurity logs it.  
- Logs are stored at:  
```
/var/log/apache2/modsec_audit.log
```

- Once verified, you can switch to **blocking mode**:
```bash
sudo nano /etc/modsecurity/modsecurity.conf
# change
SecRuleEngine DetectionOnly
# to
SecRuleEngine On
```

---

## Step 8: Next Steps
1. Configure Apache as a **reverse proxy** to your Windows DVWA VM.  
2. Test attacks from Kali Linux to verify ModSecurity blocks them.  
3. Document simulation results in `simulations/` folder (e.g., `dvwa-attacks-before.md` / `dvwa-attacks-after.md`).  

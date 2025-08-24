# Reverse Proxy Setup: ModSecurity (Ubuntu) → DVWA (Windows)

This guide configures **Ubuntu Apache + ModSecurity** as a **reverse proxy** that forwards requests to **DVWA running on Windows (XAMPP)**.  
This ensures all traffic is inspected and logged by ModSecurity.

---

## 1. Prerequisites
- Ubuntu VM with **Apache + ModSecurity** installed ✅  
- Windows VM with **XAMPP + DVWA** running ✅  
- Confirm DVWA is accessible on Windows directly via browser:  
  ```
  http://<windows-vm-ip>/DVWA
  ```

---

## 2. Enable Apache Proxy Modules on Ubuntu
Run the following on Ubuntu:

```bash
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod headers
sudo systemctl restart apache2
```

---

## 3. Configure Apache Virtual Host (Reverse Proxy)
Edit the default virtual host file:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

Replace contents with:

```apache
<VirtualHost *:80>
    ServerAdmin admin@localhost
    ServerName dvwa.lab

    # Enable reverse proxy to Windows DVWA
    ProxyPreserveHost On
    ProxyPass / http://<windows-vm-ip>/DVWA/
    ProxyPassReverse / http://<windows-vm-ip>/DVWA/

    # Ensure ModSecurity is active
    <IfModule security2_module>
        SecRuleEngine On
    </IfModule>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

👉 Replace `<windows-vm-ip>` with your Windows VM IP (e.g., `192.168.56.101`).

---

## 4. Update `/etc/hosts` (Optional)
On your **attacking machine (Kali or Host)**, map the hostname `dvwa.lab`:

```bash
sudo nano /etc/hosts
```

Add:

```
<ubuntu-vm-ip>   dvwa.lab (127.0.0.1   dvwa.local- what i used)
```

---

## 5. Restart Apache
```bash
sudo systemctl restart apache2
```

---

## 6. Test the Setup
- Open browser on Kali/Host:  
  ```
  http://dvwa.lab
  ```
- DVWA should load (served from Windows), but **all traffic is logged by ModSecurity on Ubuntu**:  
  ```
  sudo tail -f /var/log/apache2/modsec_audit.log
  ```

---

## 7. Next Steps
- Keep ModSecurity in **DetectionOnly** mode while testing.  
- Switch to **On (Prevention Mode)** later to actively block malicious requests.  
- Start launching DVWA attacks from Kali and watch **ModSecurity logs** on Ubuntu.

---

✅ You now have a **full WAF pipeline**:  
`Attacker → Ubuntu (ModSecurity) → Windows (DVWA)`  

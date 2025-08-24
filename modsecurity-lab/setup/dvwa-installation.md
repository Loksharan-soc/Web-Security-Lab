# DVWA Installation Guide (Windows VM with XAMPP)

## 📌 Prerequisites
- Windows VM installed (with network access)
- XAMPP installed (Apache + MySQL)
- Git installed (or manual zip download)

---

## 🔹 Step 1: Clone DVWA into XAMPP htdocs
Open PowerShell and run:
```powershell
cd C:\xampp\htdocs
git clone https://github.com/digininja/DVWA.git
```

If you don’t have Git, download the DVWA ZIP from GitHub and extract it into:
```
C:\xampp\htdocs\DVWA
```

---

## 🔹 Step 2: Start XAMPP Services
1. Open **XAMPP Control Panel**
2. Start **Apache** and **MySQL**

---

## 🔹 Step 3: Configure DVWA Database
1. Open browser → `http://localhost/DVWA/setup.php`
2. Click **"Create / Reset Database"**
3. If successful, the database `dvwa` will be created.

---

## 🔹 Step 4: Login to DVWA
- Go to `http://localhost/DVWA/login.php`
- Default credentials:
  ```
  Username: admin
  Password: password
  ```

---

## 🔹 Step 5: Adjust DVWA Security Settings
1. Login → Go to **DVWA Security** tab
2. Set **Security Level = Low** (for beginner testing)
3. Later, try **Medium / High** for advanced challenges

---

## ✅ Quick Test
Try a SQL Injection:
1. Navigate → **DVWA → SQL Injection**
2. Enter:
   ```sql
   1' OR '1'='1
   ```
3. If vulnerable, you’ll see multiple user records displayed.

---

## 🎯 Next Steps
- Use Kali Linux to attack DVWA (SQLi, XSS, Command Injection, etc.)
- Monitor traffic/logs from **ModSecurity (Ubuntu VM)** to detect attacks.

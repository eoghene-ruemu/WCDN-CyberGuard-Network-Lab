Purpose:
- Enumerate open ports  
- Trigger Snort portscan signatures  
- Validate detection of reconnaissance attempts  

### **5.2 Exploitation Attempts**
Tools and activities:
- Nikto web server scanning  
- Metasploit framework attempts  
- FTP brute-force simulations  
- SMB enumeration  

Snort signatures fired for:
- ET SCAN Nmap Scripting Engine  
- ET WEB_SERVER Nikto scan  
- FTP brute-force attempts  

---

## 6. Alert Collection & Analysis  

### 6.1 Snort Alerts  
- All alerts captured under **Alerts** tab  
- Classified by priority, rule, source/destination IP  
- Verified proper SID matching  

### 6.2 Log Verification  
- Alert logs cross-checked for signature integrity  
- Confirmed timestamp accuracy  
- Verified correlation with attack timestamps  

### 6.3 Pattern Recognition  
Alerts validated expected behaviors:
- Portscans  
- Web scans  
- FTP brute-force attempts  
- Command execution and exploit traffic  

---

## 7. IPS Behavior Validation  

Testing confirmed:

- Alerts triggered accurately  
- IPS mode blocked traffic where rules permitted  
- Metasploit payload attempts were partially mitigated  
- Blocked traffic appeared in pfSense system logs  

This demonstrated functional IPS enforcement.

---

## 8. Blue-Team Response Mapping  

A SOC-style response workflow was mapped:

1. **Detection**  
   Snort rule triggered → alert generated  

2. **Triage**  
   Analyst reviews priority, signature, IPs  

3. **Investigation**  
   Cross-check with Nmap/Nikto timestamps  

4. **Containment**  
   IPS blocks malicious traffic  
   Optional: pfSense firewall rule adjustments  

5. **Recovery**  
   System verified for stability  

6. **Lessons Learned**  
   Rule tuning opportunities identified  

---

## 9. Lessons Learned  

- IDS/IPS rule tuning is essential for reducing noise  
- Reconnaissance signatures fire reliably across common scans  
- pfSense provides strong baseline visibility with low overhead  
- Virtualized attack simulation enhances understanding of SOC workflows  
- Understanding signature metadata (SID, rev, msg) is crucial for triage  

---

## Summary  

The CyberGuard Network Lab successfully demonstrated foundational network security operations, including IDS/IPS deployment, firewall enforcement, attack detection, and blue-team analysis. This environment replicates core SOC responsibilities and highlights your ability to deploy, configure, and validate defensive controls in a controlled lab environment.


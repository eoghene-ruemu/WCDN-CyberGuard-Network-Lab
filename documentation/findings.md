# Findings  
## CyberGuard Network Lab  
### pfSense Firewall • Snort IDS/IPS • Threat Detection & Network Defense

This findings report summarizes the outcomes of a full network security simulation using pfSense and Snort within a controlled virtualized environment. The purpose of this lab was to evaluate firewall enforcement, intrusion detection capabilities, threat visibility, and blue-team readiness in an on-premises defensive network.

---

## 1. Overall Environment Status

### **Successful Deployment**
- pfSense firewall installed and configured as the core perimeter device.
- LAN/WAN interfaces properly assigned.
- Snort IDS/IPS installed and bound to correct interface.
- Kali Linux (attacker) and Metasploitable2 (victim) operational and reachable.
- VirtualBox networking stable across all nodes.

**Result:** Lab environment fully functional and suitable for threat simulation.

---

## 2. Firewall Functionality Findings (pfSense)

### **Strengths**
- NAT and stateful packet filtering functioning as expected.
- Default block rules correctly prevent unsolicited inbound traffic.
- System logs recorded blocked traffic events consistently.
- pfSense CPU and memory usage remained stable under load.

### **Gaps / Opportunities**
- No custom firewall policies created beyond defaults.
- No GeoIP blocking or advanced rule tuning applied.
- Logging verbosity could be improved for forensic depth.

**Impact:** Baseline firewall security strong, but could be enhanced with granular rule tuning.

---

## 3. IDS/IPS Findings (Snort)

### **3.1 Detection Effectiveness**
Snort successfully detected the following attack activities:

| Attack Type | Tool Used | Detection Triggered | Evidence |
|-------------|-----------|----------------------|----------|
| Port scanning | Nmap | ✔ ET SCAN signatures fired | Snort alerts |
| Service enumeration | Nmap NSE | ✔ ET SCAN Nmap Scripting Engine | Snort alerts |
| Web server scan | Nikto | ✔ ET WEB_SERVER Nikto Scan | Alerts log |
| FTP brute-force | Hydra (or simulated attempts) | ✔ FTP Brute-Force rules | Alerts log |
| Vulnerability probing | Metasploit | ✔ Exploit-related signatures | Snort logs |

**Outcome:** Snort reliably detected all major reconnaissance categories.

---

## 3.2 IPS Blocking Behavior
- IPS mode (inline blocking) successfully prevented certain exploit traffic.
- Blocked traffic was visible in pfSense system logs.
- IPS action depended on rule category and rule action configuration.

**Result:** IPS provided real threat prevention, not just alerting.

---

## 4. Red Team Attack Findings (Kali → Metasploitable)

### **Key Activities Detected**
- Nmap OS detection and service enumeration generated high-volume alerts.
- Nikto web scan triggered multiple critical priority rules.
- SMB and FTP probing generated authentication-related alerts.
- Exploit attempts revealed vulnerable ports but were partially blocked under IPS mode.

**Security Implication:** Detection mechanisms effectively captured reconnaissance phases that precede real-world compromises.

---

## 5. Blue Team Analysis Findings

### **Strengths**
- Alert metadata (SID, rev, signature message) provided clear triage direction.
- Source/destination IP visibility supported incident correlation.
- Timestamp alignment with attack events confirmed accurate signature firing.

### **Gaps**
- No automated log forwarding or central SIEM integration.
- No rule tuning to suppress repetitive low-value alerts.
- No severity scoring system applied to categorize findings.

**Result:** Detection was strong, but response workflow could be more structured.

---

## 6. Snort Rule Behavior & Accuracy

### **Positive Indicators**
- ET Open rules triggered correctly.
- Community rules detected broad categories of reconnaissance.
- HTTP inspection module accurately flagged web-based enumeration.

### **Limitations**
- High number of informational alerts increased noise.
- Some Snort rules generated duplicate events.
- IPS blocking selective (not universal) due to rule action settings.

**Impact:** Effective detection engine, but tuning needed for production quality.

---

## 7. System Performance Findings

### Observed
- pfSense and Snort remained stable during scans.
- No system crashes or significant latency.
- VirtualBox networks handled packet volume properly.

### Risk
- Running Snort in inline mode increases CPU load—potential future bottleneck.

---

## 8. Security Gaps & Risks Identified

| Risk | Severity | Description | Recommendation |
|------|----------|-------------|----------------|
| Noise from excessive alerts | Medium | Too many low-priority events | Rule tuning & suppression |
| No SIEM integration | High | Alerts only stored locally | Forward logs to SIEM or syslog |
| No segmentation beyond LAN/WAN | Medium | Lateral movement not tested | Add DMZ or multi-LAN segmentation |
| No automated response workflows | Medium | Manual triage only | Add scripts or SOAR mock workflows |
| Limited IPS coverage | Medium | Blocking limited by rule actions | Expand IPS-enabled rule sets |

---

## 9. Lessons Learned

- Snort requires significant tuning to reduce false positives.
- Reconnaissance traffic is the easiest and most reliably detected category.
- IPS mode is powerful but must be configured with caution.
- pfSense offers robust logging, but centralized monitoring improves analysis.
- Virtualized security labs provide realistic SOC-style investigation experience.

---

## Conclusion  

The CyberGuard Network Lab successfully demonstrated core blue-team competencies, including perimeter defense, IDS/IPS deployment, attack detection, and incident analysis. pfSense and Snort worked together to provide visibility into reconnaissance and exploitation attempts, while the Kali → Metasploitable attack chain supplied realistic data for evaluating detection effectiveness.  

Although opportunities exist for deeper automation, SIEM integration, and rule tuning, the environment met all objectives and accurately simulates foundational SOC detection engineering and network defense operations.


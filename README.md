# DetectCON 2026 – Securonix Threat Research Workshop

Welcome to the **DetectCON 2026 Securonix Workshop**! This guide covers everything you need to participate in the hands-on sessions, including platform access, case studies, and the two primary research topics: **GhostChaser** (Cyber Deception) and **PI Runner** (EDR Evasion & Detection).

---

## Instructors

| Name | Role |
|---|---|
| Akshay Gaikwad | Senior Security Researcher |
| Shikha Sangwan | Senior Security Researcher |
| Aaron Beardslee | Security Research Manager |

---

## Disclaimer

> This workshop is for **informational and research discussion purposes only**. It does not constitute a product commitment, guarantee, or contractual obligation by Securonix. Any descriptions of capabilities, research techniques, or workflows reflect current research and operational approaches, which may change without notice.
>
> Threat intelligence findings and examples are provided for **illustrative purposes only** and should not be relied upon as the sole basis for security decisions.

---

## Lab Environment Access

### Securonix SIEM Platform

| Field | Value |
|---|---|
| **URL** | https://a1t1sipi.securonix.net/Snypr |
| **Username** | `DetectCON2026` |
| **Password** | `SuperS3cr3tNinjaSqu!rrel` |

### Workshop Group

- **Group Name:** DetectCON Securonix Workshop Ninjas
- **Code:** `DetectionNinja`

---

## Case Studies

Before diving into the hands-on labs, we'll walk through two real-world threat research case studies from Securonix:

### DEAD#VAX
A threat research advisory examining a sophisticated attack campaign.

- **Blog:** https://www.securonix.com/blog/deadvax-threat-research-security-advisory/

### VOID#GEIST
An in-depth threat intelligence report on another advanced adversary.

- **Report:** https://connect.securonix.com/threat-research-intelligence-62

---

## Key Takeaway: What Do You Do When Your EDR is Bypassed?

As demonstrated in both case studies, EDR solutions are not infallible. Defense strategies should include:

- **Defense-in-depth** – layered security controls that don't rely on a single tool
- **Canaries / Deception Technologies** – high-confidence tripwires for attacker activity
- **Endpoint Monitoring with Sysmon** – detailed telemetry beyond what EDR provides
- **Community / Rapid Detection Engineering** – fast iteration on new threat indicators
- **AI-Powered Threat Hunters** – scale investigation and correlation

---

## Part 1: GhostChaser – Cyber Deception Toolkit

### What is GhostChaser?

**GhostChaser** is a Windows-based cyber deception toolkit designed to deploy and manage **"Ghosts"** — canary resources that act as tripwires across enterprise environments.

> **Important:** All techniques demonstrated by GhostChaser can be performed manually. The tool simply automates the process.

- **GitHub:** https://github.com/fluffybunnies-h4x/GhostChaser
- **Manual Walkthrough Resource:** https://github.com/fluffybunnies-h4x/CyberDeception

#### Key Capabilities

- Deploy decoy accounts, files, and network shares
- Integrate with Windows Event Logs for SIEM alerting
- Support local and remote deployment across domains

---

### The Three-Pronged Deception Architecture

GhostChaser deploys deception across three attack surfaces that adversaries commonly target during reconnaissance and lateral movement.

---

#### Strategy 1: Account Deception (Canary Accounts)

Creates realistic but enticing fake user accounts that **trigger alerts on any login attempt**.

**Deception Elements:**
- Realistic usernames: `svc_backup`, `admin_temp`, `dbadmin`
- Strong 32-character random passwords
- "Password never expires" flag (subtle attacker bait)
- Legitimate-sounding display names and descriptions
- Deployable to domain or local machines

**Detection Triggers (Windows Event IDs):**

| Event ID | Trigger |
|---|---|
| 4625 | Failed logon / credential theft attempts |
| 4625 | Brute force attacks |
| 4624 | Lateral movement with compromised credentials |
| 4624 | Pass-the-hash attacks |

**SPN Canaries (Kerberoasting Traps):**

Offensive tools like **Kerbrute** and **Rubeus** enumerate Service Principal Names (SPNs). You can plant fake SPNs as canaries:

```powershell
setspn -s fax/LOGOS.MACHINE.CITY tripmine
```

Also manipulate logon hours on ghost accounts so they can never actually log on — any successful authentication is an immediate red flag.

---

#### Strategy 2: File Deception (Canary Files)

Creates decoy documents with enticing names and realistic content that **trigger alerts when accessed**.

**Bait File Examples:**

| File | Description |
|---|---|
| `passwords.txt` | Fake authentication credentials |
| `credentials.xlsx` | CSV-formatted user/service accounts |
| `database_backup.sql` | SQL scripts with server references |
| `vpn_config.txt` | Mock VPN configuration files |
| `*.config` / `*.json` | Connection strings and app settings |

**Anti-Detection Features:**
- Backdated timestamps (3–12 months old)
- Content matches file type expectations
- Classification labels: `CONFIDENTIAL`, `RESTRICTED`

**Detection Triggers (Windows Event IDs):**

| Event ID | Trigger |
|---|---|
| 4663 | File access attempt |
| 4656 | Object handle requested |

**Example Bait Content:**

```
# TXT File
CONFIDENTIAL - Authentication Credentials Document
Primary DB: Server=sql-prod-01.internal.corp;Database=CustomerData

# JSON File
{"environment": "production", "database": {"host": "sql-prod.internal.corp"}}

# SQL File
BACKUP DATABASE [CorporateDB] TO DISK = '\\backup-server\sql-backups\'

# PowerShell Script
$ServerName = 'sql-prod.internal.corp'
$ConnectionString = 'Server=$ServerName;Integrated Security=True;'
```

**Setting Up File Auditing (Manual):**

To detect file access you must configure a **SACL (System Access Control List)** and a **GPO** for each canary file you deploy. This enables Windows to log access events to the Security Event Log.

---

#### Strategy 3: Share Deception (Honeypot Shares)

Creates realistic network shares populated with bait files that **detect network reconnaissance**.

**Share Configuration:**
- Realistic names: `Backups`, `Finance`, `HR_Documents`
- Descriptive text to appear legitimate
- Auto-populated with multiple bait file types
- Published via SMB/CIFS protocol

**Detection Capabilities:**

| Activity Detected | Event ID |
|---|---|
| Network reconnaissance scanning | 5145 |
| Unauthorized share enumeration | 5145 |
| Lateral movement attempts | 4663 |
| Persistence mechanism discovery | 4663 |

---

### Deployment Capabilities

GhostChaser supports flexible deployment scenarios:

**Local Deployment:**
- Deploy to your own machine without credentials
- Ideal for testing and validation

**Remote Deployment:**
- Deploy across the network with admin credentials
- UNC path conversion for file operations
- WMI for remote management operations

**Domain Environment:**
- Create domain accounts in specific OUs
- Support for cross-domain authentication
- Single deployment to multiple systems

**Security Features:**
- `SecureString` for password storage
- Credentials cleared after operations
- No credentials persisted to disk

---

### Detection & Monitoring

GhostChaser leverages **Windows native logging** for detection — no additional agents required.

**Windows Event Log Summary:**

| Event ID | Category | Description |
|---|---|---|
| 4624 | Account Logon | Successful logon |
| 4625 | Account Logon | Failed logon |
| 4656 | Object Access | Handle to object requested |
| 4663 | Object Access | File/Object access attempt |
| 5145 | Network Share | Network share object access check |

**SIEM Integration Points:**
- Forward Security Event Logs to your SIEM
- Alert on any ghost account logon attempt
- Alert on ghost file access patterns
- Alert on ghost share enumeration or access

---

### Other Cyber Deception Tools

GhostChaser is one of many deception tools available. Other notable options:

| Tool | URL |
|---|---|
| Thinkst Canary | https://canary.tools/ |
| Canary Tokens | https://www.canarytokens.org/nest/generate |
| Zscaler Deception | https://www.zscaler.com/products-and-solutions/deception-technology |
| AC Hunter (Active Countermeasures) | https://www.activecountermeasures.com/ac-hunter-features/cyber-deception/ |
| Tracebit | https://tracebit.com/ |
| CyberKnight | https://cyberknight.tech/vendors/attivo-networks/ |

**Training:**
- [Active Defense & Cyber Deception with John Strand – Antisyphon](https://www.antisyphontraining.com/product/active-defense-and-cyber-deception-with-john-strand/)

---

### GhostChaser Summary

**Three Detection Vectors:**
1. **Credential Theft** – Ghost accounts trigger logon events
2. **File Reconnaissance** – Ghost files trigger access logs
3. **Network Reconnaissance** – Ghost shares trigger enumeration alerts

**Key Differentiators:**
- Multi-layer deception: realistic content, timestamps, attributes
- Full automation from deployment to monitoring
- Enterprise scale with domain infrastructure support
- SIEM-ready integration via Windows Event Logs
- Secure operation with audit trails and cleanup

> **Bottom Line:** GhostChaser (and cyber deception in general) enables **proactive threat detection** by turning attacker reconnaissance tactics against them. Every ghost interaction is a **high-confidence indicator of malicious activity**.

---

## Part 2: PI Runner – Advanced EDR Evasion

### Overview

**PI Runner** is an advanced shellcode loader designed to demonstrate how modern EDR solutions can be bypassed using **legitimate mathematical computation as camouflage**.

Key characteristics:
- Uses PI calculation (Chudnovsky Algorithm) to disguise malicious activity
- Implements **word-based (jargon) obfuscation** instead of encryption to avoid cryptographic signatures
- Employs timing delays, memory evasion, and behavioral mimicry to defeat dynamic analysis

> **Research Context:** PI Runner was developed to demonstrate real attacker capabilities. If the Securonix research team can build this, nation-state threat actors and APT groups certainly can — and likely already have.

---

### Why the Chudnovsky Algorithm?

The Chudnovsky Algorithm is a legitimate, well-known formula for computing PI to high precision:

```
1/π = 12 × Σ [(-1)^k × (6k)! × (13591409 + 545140134k)] / [(3k)! × (k!)^3 × 640320^(3k+3/2)]
```

**Why this is perfect for EDR evasion:**

| Property | Evasion Benefit |
|---|---|
| Legitimately CPU-intensive | Indistinguishable from benign computation |
| Recognizable & credible algorithm | No behavioral red flags |
| Mathematically complex operations | Difficult to flag heuristically |
| Time-consuming by design | Evades sandbox timeouts |
| Established scientific use | Passes static analysis |

---

### Execution Flow & Architecture

PI Runner interleaves legitimate computation with malicious operations to appear benign at every analysis checkpoint:

```
PI Calc #1          →  Decode            →  PI Calc #2         →  Load NT API
(1,000 calcs)          (Word → Bytes)       (1,000 calcs)          (Get syscalls)

PI Calc #3          →  Alloc Memory      →  PI Calc #4         →  Copy Shellcode
(1,000 calcs)          (RW- protection)     (1,000 calcs)          (memcpy)

PI Calc #5          →  Make RX           →  Execute!
(1,000 calcs)          (Now executable)     (Payload runs)
```

> **Key Evasion:** 5 rounds of PI calculations create a **60–120+ second delay**, effectively evading most sandbox environments which time out after 30–60 seconds.

---

### Shellcode Obfuscation: Jargon Method

Instead of encrypting shellcode (which triggers cryptographic signature detections), PI Runner uses **word-based (jargon) obfuscation** — encoding shellcode as human-readable words.

**Reference:** Mike Saunders (Principal Red Teamer) – [Obfuscating Shellcode Using Jargon](https://redsiege.com/blog/2023/07/obfuscating-shellcode-using-jargon/)

---

### EDR Evasion Techniques

| Technique | Description |
|---|---|
| **Sandbox Timeout Evasion** | Long computation delays outlast sandbox analysis windows |
| **No Cryptographic Signatures** | Word-based obfuscation avoids crypto detection rules |
| **NT API Direct Syscalls** | Bypasses userland API hooks placed by EDR agents |
| **Delayed Memory Protection Change** | Memory marked executable only at the last possible moment |
| **Legitimate Process Behavior** | CPU-intensive math mimics benign workloads |
| **Thread Detachment & Persistence** | Payload survives parent process termination |

---

### EDR Impact on AV (What Happened in the Demo?)

When Crowdstrike was present alongside Windows Defender:

- Some payloads were caught by Defender; others were not
- This is due to how EDR products interact with and modify AV behavior:

| Effect | Explanation |
|---|---|
| **ELAM Priority & Resource Management** | EDR's Early Launch Anti-Malware takes priority, altering AV scan scheduling |
| **Behavioral Correlation Window Modification** | EDR changes the time window AV uses to correlate suspicious behavior |
| **API Hooking Latency** | EDR's API hooks introduce delays that affect AV detection timing |

---

### PI Runner Conclusion

**Key Takeaways:**
- Modern AV/EDR solutions **can** be bypassed
- If researchers can do it, nation-state actors and APTs absolutely can
- Defense must go beyond relying on a single EDR product

**Recommended Mitigations:**
- **Defense-in-depth** – layer your controls
- **AI-powered threat hunters** – detect behavioral anomalies EDR misses
- **Endpoint monitoring with Sysmon** – capture telemetry EDR doesn't log

---

## Summary

| Topic | Tool / Resource |
|---|---|
| Cyber Deception | [GhostChaser](https://github.com/fluffybunnies-h4x/GhostChaser) |
| Manual Deception Walkthrough | [CyberDeception Repo](https://github.com/fluffybunnies-h4x/CyberDeception) |
| SIEM Platform | https://a1t1sipi.securonix.net/Snypr |
| Case Study: DEAD#VAX | https://www.securonix.com/blog/deadvax-threat-research-security-advisory/ |
| Case Study: VOID#GEIST | https://connect.securonix.com/threat-research-intelligence-62 |
| Jargon Obfuscation Reference | https://redsiege.com/blog/2023/07/obfuscating-shellcode-using-jargon/ |
| Deception Training (Antisyphon) | https://www.antisyphontraining.com/product/active-defense-and-cyber-deception-with-john-strand/ |

---

*Thank you for attending DetectCON 2026! — Securonix Threat Research Team*

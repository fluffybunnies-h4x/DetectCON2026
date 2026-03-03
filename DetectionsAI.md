# Detections.AI – AI-Powered Detection Engineering Platform

**Platform:** [detections.ai](https://www.detections.ai/)

---

## Overview

**detections.ai** is a next-generation, community-driven detection engineering platform that combines AI-powered detection creation with a collaborative library of community-shared detection rules. It is designed to dramatically accelerate the speed at which security teams can go from raw threat intelligence to production-ready detections — shifting timelines from **days to minutes**.

The platform aggregates detection content from open-source repositories, GitHub, vendors, and individual researchers, while also providing AI tools that allow analysts to generate detection logic directly from threat intel artifacts.

> **Community Scale:** 9,000+ detection engineers across 1,500+ organizations

---

## Core Capabilities

### 1. AI-Powered Detection Creation

The flagship feature of detections.ai is its ability to take **user-provided threat intelligence** and automatically generate detection rules ready for deployment.

**Supported Intel Input Formats:**
- URLs (blog posts, threat advisories, write-ups)
- PDFs (reports, research papers)
- Documents (Markdown, JSON)

The AI models are purpose-built for detection engineering workflows — they understand threat actor TTPs, log source schemas, and detection logic patterns, producing output that is both accurate and operationally relevant.

**What the AI Does:**
- Ingests threat intelligence and extracts attacker behaviors
- Maps behaviors to relevant log sources and field names
- Generates detection logic in one or more supported formats
- Highlights logic that may need analyst review or tuning

---

### 2. Cross-Platform Detection Translation

Detections written for one SIEM or security tool can be **instantly translated** into other formats. This eliminates the manual effort of porting rules across environments.

**Some of the Supported Detection Formats:**

| Format | Platform |
|---|---|
| **Sigma** | Vendor-agnostic / universal rule format |
| **SPL** | Splunk |
| **KQL** | Microsoft Sentinel / Defender |
| **YARA-L** | Google Chronicle / SecOps |

and more...

---

### 3. Drift Awareness

Detection rules degrade over time as log schemas evolve and attack techniques change. detections.ai includes **drift awareness** — proactive monitoring that flags detection logic that has become outdated due to:

- Changes in log source field names or schemas
- Evolution in attacker TTPs
- Platform or data source version changes

This keeps your detection library fresh and reduces false negatives from stale rules.

---

### 4. Community Detection Library

detections.ai functions as a collaborative hub where the global security community can share, discover, and validate detection content.

**Content Sources:**
- Community-contributed rules
- Open-source GitHub repositories
- Vendor-published detections
- Security researchers and content creators

**Community Features:**
- **Peer review & ratings** – detections are evaluated and rated by community experts; highly-valued rules receive broad recommendations
- **Specialized groups** – join topic-focused communities such as:
  - Cloud security
  - PowerShell-based attacks
  - MITRE ATT&CK technique coverage
- **Tiered sharing** – support for both public libraries and private collections for organizations such as ISACs and Fortune 500 consortiums that need sector-specific coverage without exposing sensitive details

---

### 5. Detection Coverage

The community library and AI-generated rules cover a wide range of attack techniques, including but not limited to:

- Lateral movement
- WMI process creation
- Remote service creation
- Encoded PowerShell commands
- Credential access techniques
- Cloud-based attack patterns

---

## Intel-to-Detection Workflow

The core workflow of detections.ai is designed to be as frictionless as possible:

```
Threat Intel Source          AI Processing              Output
────────────────────    ──────────────────────    ──────────────────────
URL / Blog Post     →   Extract TTPs & IOCs   →  Sigma / SPL / KQL / YARA-L
PDF Report          →   Map to Log Sources    →  Ready-to-deploy rule
Research Document   →   Generate Logic        →  Community-shareable detection
```

1. **Provide Intel** – paste a URL, upload a PDF, or paste document content
2. **AI Extracts Behaviors** – the platform identifies attacker actions, affected systems, and relevant log sources
3. **Detection Logic Generated** – rules are produced in your target format(s)
4. **Review & Tune** – analysts validate and fine-tune before deployment
5. **Share with Community** – optionally contribute back to the community library

---

## Why This Matters for Detection Engineers

| Challenge | How detections.ai Addresses It |
|---|---|
| Detection creation is slow | AI reduces rule writing from days to minutes |
| Rules degrade over time | Drift awareness flags stale logic automatically |
| Porting rules between SIEMs is tedious | Cross-platform translation built in |
| Hard to keep up with emerging threats | Community library surfaces peer-validated detections fast |
| Limited team bandwidth | AI handles routine rule writing; humans focus on validation and hunting |

---

## Access

detections.ai operates on an **invite-based model**. You can join with an invite code or request community access directly through the platform.

- **Platform:** [https://www.detections.ai/](https://www.detections.ai/)

---

## Platform Walkthrough

### You can start creating detections with the Create With AI button
<img width="103" height="758" alt="image" src="https://github.com/user-attachments/assets/b1133703-ac2b-47c0-acce-71defa03c2ee" />

### Add your intel you want to create detections from and then click the arrow button to start building
<img width="810" height="386" alt="image" src="https://github.com/user-attachments/assets/e41141d2-b07e-4e8e-b97d-abcbcaeec385" />

### The four dots at the bottom and arrows in the upper right let you cycle through detection ideas. Click the Generate Detection button when you have chosen which detection you want to build
<img width="816" height="575" alt="image" src="https://github.com/user-attachments/assets/3ac3b63f-3c5a-4131-9dbe-3fb12b319c36" />

### When you are creating detections you have the option to choose the format (Sigma in this case) to build
<img width="826" height="125" alt="image" src="https://github.com/user-attachments/assets/c5dce2b1-7dbb-448d-a4db-e6b6d5ea99a3" />

### Once you have a detection built you can click the folder icon to save it
<img width="876" height="347" alt="image" src="https://github.com/user-attachments/assets/97fe9b27-cef2-43ca-9138-878102671f9c" />

### If you wanted to circle back to build the other detection options you can cycle through detection options on the left window pane
<img width="395" height="542" alt="image" src="https://github.com/user-attachments/assets/dcfa7a3d-9d0f-4246-b06d-0127938ba517" />

### When you generate multiple detections in a single canvas you will see tabs open up for each detection you are working on
<img width="880" height="395" alt="image" src="https://github.com/user-attachments/assets/b25a5519-a018-468c-9306-5ec8965c4d19" />

### Once you have saved one of your detection builds you can save changes to your local repo or publish to a group
<img width="671" height="324" alt="image" src="https://github.com/user-attachments/assets/cbe0a392-4f36-46ef-9639-f2061e0c056d" />

### In our case for DetectCON we will be publishing to the DetectCON Securonix Workshop Ninjas group
<img width="435" height="470" alt="image" src="https://github.com/user-attachments/assets/fe1ce0c7-c924-4057-bb91-33473ba111be" />

### Once you have published your detection you can see it in the listing of detections under the group
<img width="1398" height="644" alt="image" src="https://github.com/user-attachments/assets/cbefdfe9-32ba-4616-b5a1-b876b10e2257" />

### If you want to return to your canvas you were working on to publish more detections from a specific piece of intel you can click the vertical 3 dots icon to choose the Resume Canvas option
<img width="511" height="340" alt="image" src="https://github.com/user-attachments/assets/8439df62-7f05-42cb-b4cf-b657cec2b4ba" />

### You can also look for the clock icon in the upper left corner of the platform to view your chat history
<img width="645" height="313" alt="image" src="https://github.com/user-attachments/assets/cef50b4e-f4a8-4ee6-87e9-0c3135ba49c9" />

### This allows you to return to your previous chat canvas to continue working on that intel
<img width="340" height="374" alt="image" src="https://github.com/user-attachments/assets/e071c43a-e7c9-45be-be84-dc4f0a3be648" />

### You can also Like detections others have built if you think they are good!
<img width="951" height="532" alt="image" src="https://github.com/user-attachments/assets/85882239-9c5a-4bf0-a84b-87cd5cd4c4bc" />

### If you want to convert a detection you like to a format you can use click the Translate button when viewing a detection
<img width="306" height="315" alt="image" src="https://github.com/user-attachments/assets/75c02022-7136-4b12-aaff-93617a4b33b2" />

### When you are translating from one langauge to another you can set the target langauge from a list of options. Then click the arrow in the bottom right of that window to translate
<img width="788" height="469" alt="image" src="https://github.com/user-attachments/assets/ea84907c-9514-4277-886d-b59da5217d37" />

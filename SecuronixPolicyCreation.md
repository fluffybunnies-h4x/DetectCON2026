# Creating Policies in Securonix

**Official Documentation:** [Creating Policies – Securonix On-Prem User Guide](https://documentation.securonix.com/bundle/securonix-on-prem-user-guide/page/content/creating-policies.htm)

*Securonix On-Prem Documentation | Feb 2026*

---

## Overview

A **Policy** is the term used by Securonix to indicate the checks run on each device to detect threat indicators. Securonix applies several types of analytical techniques to detect these threat indicators.

SNYPR provides a very flexible policy engine that can be used to run checks against:

- Identity
- Access
- Events
- Resources
- Activity IP data

SNYPR comes pre-packaged with a variety of policies. For a list, see **Out-of-the-Box Policies**.

---

## Use Cases for Policies

You can use policies for the following:

- Checking for known bad signatures (rules)
- Managing separation of duties
- Checking against business-specific rules
- Managing compliance and regulatory requirements
- Detecting unusual behavior compared to a user's behavior or the behavior of their peers
- Creating policies that only apply to users from a specific location
- Generating an alert when a user performs an action that contradicts a policy

---

## How Policies Work

To create a policy, you configure **rules** that define the conditions and/or actions that constitute a violation.

**Conditional actions** allow you to specify:
- The **conditions** that must be met (e.g., the user's department or previous high-risk activity)
- The **action** that must be performed by the violation entity to trigger a violation

**Example:** A condition might check for transactions that are blocked by a firewall. The action triggered can be to:
- Perform additional analytics such as checking the data against third-party intelligence (TPI), or
- Log the event as a policy violation

> A **policy violation** occurs each time a condition set in the policy is met.

You can also specify actions that SNYPR or your SOAR tool will take when events meet the conditions and a violation is triggered.

See **Optimizing Policy Performance** for guidance on making your policies more efficient and effective.

---

## Sandbox Environment

SNYPR provides an **isolated sandbox environment** for content developers to create and test policies and threat models, without affecting the risk score of entities in the production environment.

For more information on creating policies in the Sandbox, see **Sandbox**.

---

## Policy Creation Example

---
### **Open the Menu and select Policy Violations**

<img width="652" height="326" alt="image" src="https://github.com/user-attachments/assets/412db53c-4db4-4fd8-93e1-0e95390d39f9" />


### **Click the + icon to start creating a new Policy**


<img width="412" height="158" alt="image" src="https://github.com/user-attachments/assets/94b8de81-9740-4922-a13f-7d930b065e20" />


### **Or you can create a duplicate of a policy you want to tweak**


<img width="235" height="85" alt="image" src="https://github.com/user-attachments/assets/3f5b0239-657d-46b1-ad83-2c9fc5b3b68c" />


### **Unless you have specific Datasource needs, choose Functionality**


<img width="522" height="505" alt="image" src="https://github.com/user-attachments/assets/9b87aea1-9d91-417e-884a-c45152c8b086" />


### **Add your Category, Labels and Threat Indicators**
### **Category is similar to MITRE Tactics whereas Threat Indicators are more similar to MITRE Techniques**

<img width="602" height="375" alt="image" src="https://github.com/user-attachments/assets/77e7d1a7-feaf-4579-a7b2-e2200d571efd" />


### **Click Save & Next**


<img width="1045" height="481" alt="image" src="https://github.com/user-attachments/assets/f55a4675-ebab-46e1-ae16-cb065eb34230" />


### **Individual Event Analytics are the closest to Sigma rules**


<img width="941" height="86" alt="image" src="https://github.com/user-attachments/assets/06f81589-4b46-4b34-a728-408775153e91" />


### **Click the + icon to start creating the first rule block in the Policy**


<img width="553" height="347" alt="image" src="https://github.com/user-attachments/assets/4fc1ecc0-e3df-432a-babb-4b4b41032720" />


### **The AND/OR logic between blocks and condition lines matters a LOT**


<img width="524" height="230" alt="image" src="https://github.com/user-attachments/assets/5cf8dcbc-5100-48c9-baed-27fdd6808f67" />


### **Static and Aggregate Risk scores are up to you to choose what fits your needs. Save as a threat if it's a solid detection**


<img width="508" height="431" alt="image" src="https://github.com/user-attachments/assets/7605512f-e1e7-47c8-94cf-0b270e341abb" />


### **The main Grouping Attribute is what you will see in the Violation Summary when a Policy Triggers**


<img width="828" height="406" alt="image" src="https://github.com/user-attachments/assets/e9407c7f-db36-483b-9469-64d78ec366fb" />




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

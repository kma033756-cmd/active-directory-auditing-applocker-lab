# Advanced Security Auditing, AppLocker, & Firewall Hardening Lab (`ETHA.com`)

## 📌 Project Overview
This repository documents advanced Active Directory security monitoring and endpoint hardening techniques. It covers file system access auditing, domain logon/logoff event tracking (Event IDs 4624 & 4625), AppLocker application control rules, and targeted Windows Defender Firewall GPO deployment.

## 🏗️ Environment Architecture
* **Domain Controller:** `STO-DC1` (`ETHA.com`)
* **Member Servers & Workstations:** `STO-SVR1`, `STO-CORE`, `STO-CL1`
* **Core Tools:** Group Policy Management Console (GPMC), Event Viewer, Advanced Security Auditing
* **Domain Functional Level:** Windows Server 2025

---

## ⚙️ Key Tasks & Technical Implementation

### 1. File System Access Auditing
* Configured object access auditing policies within the **Member Server Security Settings** GPO[cite: 4].
* Enabled shared folder auditing on the `Marketing` share for `Domain Users` to track read/write attempts[cite: 4].
* Verified and investigated security event handles (`Event ID 4658`) via Event Viewer on `STO-SVR1`[cite: 4].

### 2. Domain Logon & Security Event Monitoring
* Implemented domain-wide GPOs for **Audit Logon / Logoff** events to capture successful and failed authentication attempts[cite: 4].
* Simulated brute-force login attempts with incorrect credentials on client node `STO-CL1` and successfully tracked audit failures (`Event ID 4625`) versus successful logins (`Event ID 4624`) on domain controller `STO-DC1`[cite: 4].

### 3. Application Control via AppLocker Policies
* Created a dedicated `Client Computers` OU, migrated client asset `STO-CL1`, and established a **Software Control** GPO[cite: 4].
* Configured and enforced **AppLocker** executable rules and path-based permissions (allowing standard utilities like WordPad while blocking unapproved software paths)[cite: 4].
* Verified block logs (`Event ID 8002`) and system integrity rules in the Event Viewer[cite: 4].

### 4. Network Traffic Securing with Windows Defender Firewall
* Created an **Application Servers** security group and added `STO-SVR1` as a member[cite: 4].
* Deployed an **Application Servers Firewall GPO** linked to the `Member Servers` OU, utilizing security filtering to apply specific inbound port rules (e.g., TCP port 8080) strictly to target application servers[cite: 4].

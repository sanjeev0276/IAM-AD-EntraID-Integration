# IAM AD-EntraID Integration Project
![Active Directory](https://img.shields.io/badge/Active%20Directory-On--Prem%20Identity-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Microsoft Entra ID](https://img.shields.io/badge/Microsoft%20Entra%20ID-Hybrid%20Identity-0078D4?style=for-the-badge&logo=microsoftentraid&logoColor=white)
![RBAC](https://img.shields.io/badge/RBAC-Role%20Engineering%20%26%20Access%20Governance-2E86C1?style=for-the-badge)
![Offboarding](https://img.shields.io/badge/Offboarding-Access%20Revocation-6C3483?style=for-the-badge)
![PowerShell](https://img.shields.io/badge/PowerShell-Automation%20%26%20Investigation-5391FE?style=for-the-badge&logo=powershell&logoColor=white)

**Author:** Sanjeev Shrestha | Dallas–Fort Worth Area, TX (Shrestha Technologies)  
**Target Roles:** IAM Engineer / Identity Engineer / Entra ID Engineer (2027)  
**Certification Focus:** Preparing for Microsoft SC-300: Identity and Access Administrator Associate <br>
**Environment:** Microsoft Active Directory/Entra ID

## 5 Labs Architecture Overview
 ![Architecture_Overview](Overall_Architecture_Diagram.png)

## Quick Navigation and Lab Execution Status
<a id="lab-execution-status"></a>
| Lab       | Focus Area                                | Status    | Jump to Lab                                                                  |
|-----------|-------------------------------------------|-----------|------------------------------------------------------------------------------|
| **Lab 1** | AD Foundation | Completed | [Go to Lab 1 >>](#lab-1-okta-tenant-setup--configuration)                       |
| **Lab 2** | RBAC | Completed | [Go to Lab 2 >>](#lab-2-active-directory-integration--delegated-authentication) |
| **Lab 3** | Offboarding | Completed | [Go to Lab 3 >>](#lab-3-rbac-design--access-sprawl-investigation)               |
| **Lab 4** | Lockout  | Completed | [Go to Lab 4 >>](#lab-4-saml-20-application-integration)                        |
| **Lab 5** | Entra Connect  | Completed | [Go to Lab 5 >>](#lab-5-adaptive-mfa-step-up-authentication--zero-trust)        |

---
## Executive Summary and Business Impact
Built a hybrid identity environment using Active Directory, Microsoft Entra ID, RBAC, PowerShell, and Entra Connect across five hands-on labs.
- **Identity Administration:** Implemented OU design, group-based access, and least-privilege controls.
- **Access Management:** Designed RBAC and segregation-of-duties (SoD) controls.
- **Identity Lifecycle:** Performed secure offboarding and access revocation with audit tracking.
- **Security Operations:** Investigated account lockouts and password-spray activity using Event Logs and PowerShell.
- **Hybrid Identity:** Configured Entra Connect synchronization between on-prem AD and Entra ID.
- **Business Impact:** Reduced access risk, strengthened governance, and improved operational efficiency.
---
## Key Skills Demonstrated
- Active Directory Administration & Hybrid Identity
- Role-Based Access Control (RBAC) & Segregation of Duties (SoD)
- Identity Lifecycle Management (Provisioning, Deprovisioning, Offboarding)
- Access Governance & Certification
- PowerShell Automation & Security Investigations
- Microsoft Entra Connect & Directory Synchronization
## Technologies Used
| Category | Technologies |
|-----------|-------------|
| Identity Platforms | Active Directory, Microsoft Entra ID, VMware Workstation, Windows Server 2022 |
| Directory Synchronization | Microsoft Entra Connect |
| Access Management | RBAC, SoD |
| Identity Lifecycle | Provisioning, Deprovisioning |
| Automation | PowerShell |
## Detailed Lab Implementations and Visual Proof
<a id="lab-1-okta-tenant-setup--configuration"></a>
### Lab 1: AD Foundation

**Key Learnings and Takeaways:**
* Plan for leavers, not just joiners Disabled accounts need their own OU. It keeps terminated users isolated, easy to audit, and out of sync.
* Give access to groups, not people When access lives in groups, moves and exits become a membership change, not a cleanup project.
* Don't sync everything to the cloud If an account shouldn't have access, it shouldn't sync to Entra ID either.

<details>
<summary>📸 <b>Click here to view Lab 1 Diagrams and Screenshots >></b></summary>

<br>

#### Architecture Diagram
![Architecture Diagram](Lab01-AD-Foundation/Screenshots/Architecture_Diagram.png)

#### AD Foundation
* **Environment:**  
  ![Environment](Lab01-AD-Foundation/Screenshots/Static-IP-192.168.10.10.png)
* **ADUC OU Tree:**  
  ![People](Lab01-AD-Foundation/Screenshots/ADUC-OU-Tree.png)
* **Groups-Finance-SoD:**  
  ![Groups-Finance-SoD](Lab01-AD-Foundation/Screenshots/Groups-Finance-SoD.png)
* **Marcus-Williams:**  
  ![Marcus-Williams](Lab01-AD-Foundation/Screenshots/Marcus-Williams.png)
* **Jessica-Park:**  
  ![Jessica-Park](Lab01-AD-Foundation/Screenshots/Jessica-Park.png)
* **Jessica-Park-Expiry:**  
  ![Jessica-Park-Expiry](Lab01-AD-Foundation/Screenshots/Jessica-Park-Expiry.png)

</details>

---
**[↑ Back to Lab Execution Status](#lab-execution-status)**

<a id="lab-2-active-directory-integration--delegated-authentication"></a>
### Lab 2: RBAC

**Key Learnings and Takeaways:**
* Design before you build - If it's not in the matrix, don't build it. If you built it but it's not in the matrix, that's an audit finding.
* The matrix is the contract - Map each role to systems like — AD, Email, FinanceCore, PeopleHub, SalesPro, — plus Invoice Create / Approve / Admin. Every cell gets Allow, Deny, or Read-Only.
* SoD stops fraud, not just paperwork - Define the conflicts before we build.

<details>
<summary>📸 <b>Click here to view Lab 2 Diagrams and Screenshots >></b></summary>

<br>

#### Architecture Diagram
![Architecture Diagram](Lab02-RBAC/Screenshots/Architecture_diagram.png)

#### RBAC Proof
* **SoD Policy:**  
  ![SoD Policy](Lab02-RBAC/Screenshots/SoD-Policy.png)
* **Privilege Creep - Before remediation :**  
  ![Before-remediation ](Lab02-RBAC/Screenshots/Before-remediation.png)
* **After remediation:**  
  ![After-remediation](Lab02-RBAC/Screenshots/After-remediation.png)
* **Role Change:**  
  ![Role-Change](Lab02-RBAC/Screenshots/Role-Change.png)
* **Access Certification:**  
  ![Access-Certification](Lab02-RBAC/Screenshots/Access-Certification.png)
* **Threat Connections:**  
  ![Threat-Connections](Lab02-RBAC/Screenshots/Threat-Connections.png)
  
</details>

---
**[↑ Back to Lab Execution Status](#lab-execution-status)**

<a id="lab-3-rbac-design--access-sprawl-investigation"></a>
### Lab 3: Offboarding

**Key Learnings and Takeaways:**
* Offboarding is a security process, not just an HR task. Disabled accounts and access removal help prevent unauthorized access after an employee leaves.
* Documenting every action is important. Maintaining a provisioning/deprovisioning log creates an audit trail and supports compliance reviews.
* Verify access is actually removed. Don't assume access is gone. Check group memberships, accounts, and permissions to confirm deprovisioning was successful.

<details>
<summary>📸 <b>Click here to view Lab 3 Diagrams and Screenshots >></b></summary>

<br>

#### Architecture Diagram
![Architecture Diagram](Lab03-Offboarding/Screenshots/Architecture_Diagram.png)

#### Offboarding Proof
* **Before Leaver Active:**  
  ![Before-Leaver-Active](Lab03-Offboarding/Screenshots/Before-Leaver-Active.png)
* **After Disabled And Moved:**  
  ![After-Disabled-And-Moved](Lab03-Offboarding/Screenshots/After-Disabled-And-Moved.png)
* **After-No-Groups:**  
  ![After-No-Groups](Lab03-Offboarding/Screenshots/After-No-Groups.png)

</details>

---
**[↑ Back to Lab Execution Status](#lab-execution-status)**

<a id="lab-4-saml-20-application-integration"></a>
### Lab 4: Lockout

**Key Learnings and Takeaways:**
* Same lockout, 3 different stories One person forgetting a password looks the same as an attack — until you check the pattern. One account = typo. One account failing super fast = old password stuck somewhere. Three accounts failing at the same time = someone spraying passwords. Don't just unlock. Figure out which one it is first.
* Two logs tell the full story 4740 tells you who got locked. 4625 tells you why and from where. One without the other is just a guess. Always check both before you decide if it's routine or serious.
* You can't spot an attack by scrolling Scrolling Event Viewer one by one will never show you a spray. Grouping the failures by account in PowerShell will — when three accounts suddenly have the exact same number of fails, that's the attack.

<details>
<summary>📸 <b>Click here to view Lab 4 Diagrams and Screenshots >></b></summary>

<br>

#### Architecture Diagram
![Architecture Diagram](Lab04-Lockout/Screenshots/Architecture_Diagram.png)

#### Lockout Proof
* **Audit Policy Configuration:**  
  ![Audit Policy Configuration](Lab04-Lockout/Screenshots/Audit_Policy_Configuration.png)   
* **Scenario A — Marcus Williams — Simple Password Mistake**  
  ![Scenario_A](Lab04-Lockout/Screenshots/Scenario_A.png) 
* **Scenario B — David Osei — Stale Cached Credentials:**  
  ![Scenario_B](Lab04-Lockout/Screenshots/Scenario_B.png)
* **Scenario C — Linda Okafor, Rachel Thompson, Michael Obi — Spray Pattern:**  
  ![Scenario_C](Lab04-Lockout/Screenshots/Scenario_C.png) 

</details>

---
**[↑ Back to Lab Execution Status](#lab-execution-status)**

<a id="lab-5-adaptive-mfa-step-up-authentication--zero-trust"></a>
### Lab 5: Entra Connect

**Key Learnings and Takeaways:**
* Microsoft Entra Connect bridges on-prem Active Directory and Entra ID.
* Hybrid identity provides one consistent identity across on-prem and cloud systems.
* Automated synchronization improves security, user lifecycle management, and operational efficiency.

<details>
<summary>📸 <b>Click here to view Lab 5 Diagrams and Screenshots >></b></summary>

<br>

#### Architecture Diagram
![Architecture Diagram](Lab05-Entra-Connect/Screenshots/Architecture_Diagram.png)

#### Entra Connect AD Directories 
* **Entra Connect AD Directories 1:**  
  ![Entra_Connect_AD_Directories_1](Lab05-Entra-Connect/Screenshots/Entra_Connect_AD_Directories_1.png)  
 
* **Entra_Connect_AD_Directories_2:**  
  ![Entra_Connect_AD_Directories_2](Lab05-Entra-Connect/Screenshots/Entra_Connect_AD_Directories_2.png)  
* **Entra_Connect_AD_Directories_3:**  
  ![Entra_Connect_AD_Directories_3](Lab05-Entra-Connect/Screenshots/Entra_Connect_AD_Directories_3.png) 
* **Entra-Sign-In-Config-Not-Added:**  
  ![Entra-Sign-In-Config-Not-Added](Lab05-Entra-Connect/Screenshots/Entra-Sign-In-Config-Not-Added.png)
* **Domain-OU-Filtering:**  
  ![Domain-OU-Filtering](Lab05-Entra-Connect/Screenshots/Domain-OU-Filtering.png)   
* **Filtering-Disabled-Unchecked:**  
  ![Filtering-Disabled-Unchecked](Lab05-Entra-Connect/Screenshots/Filtering-Disabled-Unchecked.png)
* **Uniquely-Identifying-Users:**  
  ![Uniquely-Identifying-Users](Lab05-Entra-Connect/Screenshots/Uniquely-Identifying-Users.png)
* **Filter-Users-Devices-All:**  
  ![Filter-Users-Devices-All](Lab05-Entra-Connect/Screenshots/Filter-Users-Devices-All.png)
* **Optional Features — Reviewed, Not Enabled (Free Tier):**  
  ![Optional-Features-Password-Writeback](Lab05-Entra-Connect/Screenshots/Optional-Features-Password-Writeback.png)
* **Ready-To-Configure-Summary:**  
  ![Ready-To-Configure-Summary](Lab05-Entra-Connect/Screenshots/Ready-To-Configure-Summary.png)
* **Configuration-Complete:**  
  ![Configuration-Complete](Lab05-Entra-Connect/Screenshots/Configuration-Complete.png)
* **Sync-Operations-All-Success:**  
  ![Sync-Operations-All-Success](Lab05-Entra-Connect/Screenshots/Sync-Operations-All-Success.png)
* **Entra-Users-Synced-OnPrem-Yes:**  
  ![Entra-Users-Synced-OnPrem-Yes](Lab05-Entra-Connect/Screenshots/Entra-Users-Synced-OnPrem-Yes.png)                    

</details>

---
**[↑ Back to Lab Execution Status](#lab-execution-status)**

## Original Repository and Credits
This hands-on lab series was adapted and built upon the foundational framework provided by [okpe027/IAM-HomeLab-Portfolio](https://github.com/okpe027/IAM-HomeLab-Portfolio/tree/main). 

### What I adapted:
- Lab structure and overall flow

### What I built / added myself:
- Added Overall Architectural diagram, and each lab architecture diagram.
- Rewrote RBAC matrix for 50 users.
- Added PowerShell automation scripts.
- Added screenshots and validation steps.
- All configurations, testing, and documentation in this repo.
  
Original work remains credited to its author. This repo is my hands-on implementation and extension of that framework.








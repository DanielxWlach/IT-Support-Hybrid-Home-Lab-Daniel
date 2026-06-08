# IT-Support-Hybrid-Home-Lab-Daniel
Personal Home Lab of Daniel Wlach
# Hybrid IT Support Home Lab Portfolio
## Overview
An enterprise-grade sandbox integrating an on-premises Windows Server 2022 domain environment with Microsoft 365 Cloud Architecture, Entra ID, and Intune Endpoint Management.

## Lab Topology
* [Insert Lab Diagram Here]

## Milestones Documented
- [x] Phase 1: M365 Cloud Sandbox Setup & User Provisioning
- [x] Phase 2: Local Hypervisor & Server Deployment
- [x] Phase 3: Active Directory Domain Services Setup
- [x] Phase 4: Hybrid Cloud Sync & Intune Enrollment
- [ ] Phase 5: Advanced Systems Engineering & Help Desk Operations Staging

### Phase 1 Implementation Evidence
   Here is the pristine Hyper-V virtualization host environment initialized on the host laptop before OS deployment:
   
   ![Hyper-V Blank Environment Canvas](HyperV_Blank.png)

### Phase 2 Implementation Evidence
   Here is the live deployment of the Windows Server 2022 base environment running inside Hyper-V:
   
   ![Windows Server 2022 Base Installation](VM_running.png)

### Phase 3 Implementation Evidence
     Successfully promoted the standalone server to a Root Domain Controller, establishing the local directory database:
![Active Directory Domain Controller Setup](active-directory-setup.png)


### Phase 4 Implementation Evidence

To simulate a real-world corporate onboarding and system administration scenario, I implemented user management lifecycle standards and enterprise baseline security.

#### 1. Directory Structure & Workforce Provisioning
I structured the corporate environment using Organizational Units (OUs) and provisioned a team of 5 fictional employees. Following identity and access management (IAM) best practices, every user account was built with a temporary credential requiring a forced password reset upon their very first login.

![Forced Password Reset Policy](user-password-policy.png)

#### 2. Administrative Data Tracking
To maintain strict data integrity and assist with identity auditing, I developed a centralized employee tracking matrix detailing fictional personnel demographics, corporate email mapping, start dates, and initial credential cycles.

![Fictional HR Data Tracker](hr-employee-tracker.png)

#### 3. Enterprise Group Policy Enforcement
To secure corporate workstations against physical data exposure, I engineered a domain-wide Group Policy Object (GPO) titled `Corp_Security_ScreenLockout`. This policy targets user objects to automatically enforce a 15-minute (900 seconds) idle screen saver timeout and automated desktop lock.

Below is the live operational environment showing the 5 active user objects alongside the active, enabled Group Policy configuration:

![Active Workforce and Group Policy Management](workforce-and-gpo.png)



## 🛠️ Advanced IT Infrastructure Optimization & Help Desk Operations

To elevate this environment beyond a basic out-of-the-box configuration, this section details production-grade systems engineering implementations designed to enforce organizational compliance, optimize user workflows, and establish enterprise desktop baselines.

### 📋 Section 1: Advanced Systems Engineering (Group Policy Objects)

#### 1. Automated Enterprise Network Drive Mapping (`GPO 1`)
* **Business Requirement:** The organization requires a standardized, centralized network storage repository accessible to all corporate personnel immediately upon session initialization. Handkeying network paths on individual client devices introduces operational overhead and potential security configuration drift.
* **Engineering Solution:** Architected a dedicated, domain-wide Group Policy Object titled `Corp_Preferences_DriveMapping`. Rather than embedding preferences within unrelated security objects, this modular preference explicitly maps the corporate file share repository to the uniform network drive letter `Z:\`.
* **Technical Implementation Path:** Navigated via `User Configuration` ➔ `Preferences` ➔ `Windows Settings` ➔ `Drive Maps`. Configured an `Update` action targeting the network share path (`\\DC-SERVER-2022\CompanyShare`) utilizing standard inheritance rules linked directly to the workforce Organizational Unit (OU).

Below is the verified staging environment demonstrating the active object configuration and path targets:

![Group Policy Management Editor - Drive Maps](drive_map.png)

The granular deployment matrix properties enforced within the target environment:

![Z: Drive Properties Mapping Details](drive_map_2.png)

---

#### 2. Enterprise Desktop Environment Standardization (`GPO 2`)
* **Business Requirement:** Corporate branding guidelines dictate a uniform desktop environment across all operational endpoints. Allowing end-users to customize workspace backgrounds introduces visual non-compliance and potential exposure to unvetted imagery within customer-facing environments.
* **Engineering Solution:** Implemented a granular environment constraint titled `Corp_Preferences_DesktopWallpaper` targeted directly at the workforce container.
* **Technical Implementation Path:** Governed via `User Configuration` ➔ `Policies` ➔ `Administrative Templates` ➔ `Desktop` ➔ `Desktop`. Enforced the `Desktop Wallpaper` policy to state `Enabled`, pointing configuration parameters to a static system resource path (`C:\Windows\Web\Wallpaper\Windows\img0.jpg`) utilizing a unified `Fill` style matrix.

Below is the verified administrative template blueprint enforcing endpoint visual conformity:

![Desktop Wallpaper GPO Configuration](wallpaper_gpo.jpg)

---

#### 3. Endpoint Hardening & Access Control (`GPO 3`)
* **Business Requirement:** Mitigate the internal attack surface by preventing standard non-administrative personnel from accessing local CLI environments. Restricting interactive command execution drastically reduces the success rate of malicious pivot scripts, reconnaissance commands, and unauthorized system modifications.
* **Engineering Solution:** Established a strict security baseline policy titled `Corp_Security_RestrictCMD` linked explicitly to standard user profiles.
* **Technical Implementation Path:** Navigated via `User Configuration` ➔ `Policies` ➔ `Administrative Templates` ➔ `System`. Toggled the `Prevent access to the command prompt` constraint to `Enabled`.
* **Granular Constraint Justification (Script Processing Selection):** Within the policy configurations, the parameter *“Disable the command prompt script processing also?”* was intentionally designated as **`No`**. 
  * *Architectural Logic:* Setting this constraint to **`No`** prevents standard users from interactively launching `cmd.exe` to execute manual commands, but crucially **preserves the operating system's ability to run legitimate logon, logoff, or deployment scripts in the background**. This ensures that administrative automation, mapping scripts, and security agents run seamlessly at startup without breaking core IT operational capabilities.

Below is the hardened policy profile demonstrating interactive restriction paired with background script preservation:

![Command Prompt Access Restriction GPO](restrict_cmd_gpo.jpg)



### ⏳ [In Progress] Pending Infrastructure Implementations & Help Desk Ticket Ledger
* 🔲 **Ticket #1042:** User Account Lockout Remediation & Credential Cycle Lifecycle
* 🔲 **Ticket #1043:** Corrupted Client-Side Name Resolution (DNS) Flushing & Validation
* 🔲 **Ticket #1044:** Force Propagation of Active Directory Security Policies via CLI Tools

     
     


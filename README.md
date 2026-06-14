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
- [x] Phase 5: Advanced Systems Engineering & Help Desk Operations Staging

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

![Desktop Wallpaper GPO Configuration](wallpaper_gpo.png)

---

#### 3. Endpoint Hardening & Access Control (`GPO 3`)
* **Business Requirement:** Mitigate the internal attack surface by preventing standard non-administrative personnel from accessing local CLI environments. Restricting interactive command execution drastically reduces the success rate of malicious pivot scripts, reconnaissance commands, and unauthorized system modifications.
* **Engineering Solution:** Established a strict security baseline policy titled `Corp_Security_RestrictCMD` linked explicitly to standard user profiles.
* **Technical Implementation Path:** Navigated via `User Configuration` ➔ `Policies` ➔ `Administrative Templates` ➔ `System`. Toggled the `Prevent access to the command prompt` constraint to `Enabled`.
* **Granular Constraint Justification (Script Processing Selection):** Within the policy configurations, the parameter *“Disable the command prompt script processing also?”* was intentionally designated as **`No`**. 
  * *Architectural Logic:* Setting this constraint to **`No`** prevents standard users from interactively launching `cmd.exe` to execute manual commands, but crucially **preserves the operating system's ability to run legitimate logon, logoff, or deployment scripts in the background**. This ensures that administrative automation, mapping scripts, and security agents run seamlessly at startup without breaking core IT operational capabilities.

Below is the hardened policy profile demonstrating interactive restriction paired with background script preservation:

![Command Prompt Access Restriction GPO](restrict_cmd_gpo.png)


#### 🛠️ Ticket #1042: Active Directory Identity Access & Account Lifecycle Activation
* **ITSM Platform Environment:** Spiceworks Cloud Help Desk Portal
* **Incident Urgency/Priority:** Medium / P3 (Standard Identity Lifecycle Request)
* **Target Identity Object:** `User: John Smith | OU: Staff | Domain: NEXTTECHX.local`
* **Symptoms/Request Reported:** HR/Management submitted an operational request to reinstate systems access for returning personnel John Smith. The user identity object was flagged with a hard local restriction: *"Your account has been disabled. Please see your system administrator."*

Below is the active Spiceworks lifecycle tracking ticket managed for this request:

![Spiceworks Identity Management Ticket](spiceworks_ticket_1.png)

* **Diagnostic & Technical Remediations:**
  1. Logged into the Windows Server 2022 Domain Controller staging environment and initiated the **Active Directory Users and Computers (ADUC)** management console.
  2. Traversed the organizational directory layout to locate the deactivated user target object within the designated `Staff` OU.
  3. Audited account security attributes to verify the structural state of the object profile.
  4. Executed identity remediation by clearing the `Account is disabled` structural constraint within the Security Principal Account options matrix, restoring active domain privileges.

Below is the verified administrative intervention re-enabling the directory services object within Active Directory:

![Active Directory Account Status Modification](enable_account.png)

* **Root Cause/Operational Determination:** The account state was confirmed as an intentional administrative deactivation used during a standard personnel contract pause. The restriction has been lifted, authentication paths have been verified, and the tracking ticket has been successfully resolved and archived.

Below is the verified Spiceworks ledger entry confirming the incident has been moved to a closed operational state:

![Spiceworks Closed Ticket Resolution Status](spicework_ticket_1_closed.png)


#### 🛠️ Ticket #1043: Client-Side Name Resolution (DNS) Corruption & Stale Cache Remediation
* **ITSM Platform Environment:** Spiceworks Cloud Help Desk Portal
* **Incident Urgency/Priority:** High / P2 (Workstation Network Isolation / Local Intranet Inaccessible)
* **Target Identity Object:** `User: Anna Heart | OU: Staff | Device: NTX-CL-05`
* **Symptoms Reported:** End-user reported total inability to resolve internal domain web assets (`portal.nexttechx.local`) and external web gateways. Diagnostic isolation confirmed neighboring endpoints on the same subnet were unaffected, pointing directly to a client-specific stack degradation.

Below is the active Spiceworks lifecycle tracking ticket initiated for this incident:

![Spiceworks DNS Trouble Ticket](spiceworks_ticket_2.png)

* **Diagnostic & Technical Remediations:**
  1. Initiated remote administrative CLI access on the target workstation asset (`NTX-CL-05`).
  2. Executed a complete purge of the locally cached, potentially poisoned or stale address resolution table using the Windows IP configuration utility:
     ```cmd
     ipconfig /flushdns
     ```
  3. Triggered manual refresh serialization to force the endpoint to re-register its host boundaries with the local Active Directory Domain Controller DNS zone files:
     ```cmd
     ipconfig /registerdns
     ```
  4. Verified successful resolution integrity by executing a network echo test (`ping`) against the target intranet header.

Below is the verified client-side resolution pipeline executed to remediate the cached network state:

![Command Prompt DNS Cache Flush Execution](dns_flush.png)

* **Root Cause Determination:** Technical analysis indicated local DNS resolver cache corruption. The endpoint had cached a stale IP mapping during an ungraceful lease renewal cycle, preventing correct packet routing. The records were successfully purged, and the tracking ticket has been closed and archived.

Below is the verified Spiceworks ledger entry confirming the networking incident has been resolved:

![Spiceworks Closed DNS Ticket Resolution](spiceworks_ticket_2_closed.png)


### 🚨 Bonus Showcase: Hyper-V Host Resource Contention Troubleshooting
* **Infrastructure Exception:** Virtual Machine State Change Failure (`Error Code: 0x800705AA`)
* **Environment Context:** Local Host System (Type-2 Hypervisor Layer) executing `DC-Server-2022`
* **Symptoms Identified:** Triggering the execution state on the Domain Controller dropped a hard hypervisor intercept fault: *"Unable to allocate 2560 MB of RAM: Insufficient system resources exist."*

Below is the verified resource depletion error intercepted during the lab initialization phase:

![Hyper-V Resource Allocation Error](Storage_issue.png)

* **Root Cause Diagnostics:** The physical host system experienced RAM exhaustion due to concurrent background operational processes. The hypervisor layer intentionally denied the VM boot request to prevent host OS instability or a Blue Screen of Death (BSOD) caused by memory starvation.
* **Engineering Resolution Matrix:** 1. Gracefully terminated unnecessary high-overhead consumer processes on the parent host to reclaim hardware pages.
  2. Navigated to `Hyper-V Manager` ➔ `DC-Server-2022 Settings` ➔ `Memory Properties`.
  3. Reconfigured the hypervisor's memory allocation strategy by enabling **Dynamic Memory provisioning**. 
  4. Adjusted the absolute `Startup RAM` floor matrix to a lower boundary conditions threshold ($2048\text{ MB}$ initialization base, down-scaling to a minimum active footprint of $1024\text{ MB}$).

Below is the verified hardware configuration adjustments applied inside Hyper-V Manager to optimize host memory distribution:

![Hyper-V Memory Optimization Settings](hyperv_memory_fix.png)
  
* **Outcome:** The memory provisioning optimization bypassed the host contention ceiling, allowing the Domain Controller to successfully achieve an active operational state without starving the host OS.


#### 🛠️ Ticket #1044: Active Directory Group Policy (GPO) Non-Propagation & Client-Side Refresh
* **ITSM Platform Environment:** Spiceworks Cloud Help Desk Portal
* **Incident Urgency/Priority:** Medium / P3 (Compliance Deficiency / Non-Applied Security Configuration)
* **Target Identity Object:** `User: Alex Junior | OU: Staff | Device: NTX-CL-11`
* **Symptoms Reported:** End-user Alex Junior reported that newly deployed administrative restrictions (specifically the corporate desktop interactive execution constraints) were not active on the workstation local shell context, exposing an enterprise compliance gap.

Below is the active Spiceworks lifecycle tracking ticket initiated for this incident:

![Spiceworks GPO Trouble Ticket](spiceworks_ticket_gpo.png)

* **Environmental Defect Encountered:** Upon accessing the terminal environment to execute the refresh command natively (`gpupdate /force`), the local Windows shell threw a standard execution error: *" 'gpupdate' is not recognized as an internal or external command, operable program or batch file."* This behavior indicated an environment `%PATH%` variable resolution disruption on the target endpoint.

Below is the verified terminal path execution exception captured during diagnostics:

![Command Prompt Environment Path Error](mmm.png)

* **Diagnostic & Technical Remediations:**
  1. Overrode the system environment variable parsing failure by targeting the absolute local root system file path directly where the deployment utility resides.
  2. Bypassed the tracking failure by executing the explicit drive string path to successfully kick off immediate policy evaluation:
     ```cmd
     C:\Windows\System32\gpupdate.exe /force
     ```
  3. Audited the client-side Resultant Set of Policy (RSoP) matrix to confirm successful receipt of user-context objects and computer-context configurations using the core infrastructure reporting utility:
     ```cmd
     C:\Windows\System32\gpresult.exe /r
     ```
  4. Confirmed that target security objects (`Corp_Security_Policy`) shifted explicitly into the active `Applied Group Policy Objects` registry table.

Below is the verified terminal screenshot displaying the successful policy force using the absolute system file string path:

![Command Prompt Absolute Path GPO Force](gpo_update.png)

* **Root Cause Determination:** The client endpoint failed to apply background policies automatically due to an environment path corruption blocking native command shortcuts. Bypassing the path via the absolute system directory successfully forced immediate policy synchronization from the primary Domain Controller database. The asset is verified compliant, and the tracking ticket has been closed and archived.

Below is the verified Spiceworks ledger entry confirming resolution fulfillment and archiving:

![Spiceworks Closed GPO Ticket Resolution](spiceworks_gpo_closed.png)



---

### 🤖 Phase 3: PDirectory Automation & Bulk Identity Provisioning (PowerShell)
* **Infrastructure Layer:** Automated Directory Database Manipulation (IAM)
* **Automation Tooling:** PowerShell Scripting Engine / ActiveDirectory Module
* **Operational Scope:** Scalable User Lifecycle Management & Automated HR Integration

#### 🌐 Architectural Overview
To demonstrate competency in scalable enterprise workflows, manual GUI object creation was replaced with automated pipeline processing. A custom PowerShell scripting deployment was engineered to parse incoming HR data streams (`.csv`) and programmatically provision directory records under structured corporate compliance boundaries.

Below is the raw human resources data roster staged inside Notepad prior to pipeline processing:

![Staged HR CSV Employee Roster](notepad_script.png)

Below is the verified operational script and output execution log successfully processing database identities:

![PowerShell Bulk User Provisioning Deployment](powershell_script.jpg)

#### 🛠️ Automation Logic & Parameters
1. **Data Parsing:** Script ingests raw data headers (`FirstName`, `LastName`, `Department`, `Title`) to eliminate manual data entry human error.
2. **String Interpolation:** Automatically structures standardized enterprise naming matrices, generating the unique User Principal Name (`first.last@nexttechx.local`) and localized SAM accounts.
3. **Security Baselines:** Injects an identity security floor by assigning cryptographically masked default credentials while simultaneously enforcing the `ChangePasswordAtLogon` policy restriction.
4. **Target Routing:** Directly maps and drops structural principal accounts into their designated target organizational container.

#### 🔍 Environmental Troubleshooting & Path Resolution
* **Directory Path Debugging Exception:** Initial execution yielded delivery faults due to an organizational directory path structural mismatch. The target active environment utilized a nested root design schema rather than a flat baseline layout.
* **Remediation Resolution:** Intercepted the failure sequence by analyzing the directory hierarchy within the ADUC management console. Reconfigured the deployment string variable parameter from a flat path directly to the explicit nested container destination query: 

```markdown

```powershell
$TargetOU = "OU=Staff,OU=Corp_Root,DC=NextTechX,DC=local"
```



![Active Directory Bulk Onboarding Results](aduc_bulk_result.jpg)


---

### 🛡️ Phase 4: Role-Based Access Control (RBAC) & Network File Share Governance
* **Infrastructure Layer:** Secured Distributed Storage Architecture (Data Security)
* **Access Control Methodology:** Principle of Least Privilege (PoLP) via NTFS Discretionary Access Control Lists (DACLs)
* **Operational Scope:** Structural Security Group Provisioning and Multi-Departmental Share Isolation

#### 🌐 Architectural Overview
To implement enterprise-grade data security baselines, a role-based access management framework was engineered on the storage tier. Moving away from highly inefficient individual user permission mappings, the directory architecture was grouped by departmental boundaries utilizing Active Directory Security Groups. This infrastructure limits cross-departmental data exposure and establishes strict governance over local network assets.

Below is the active directory state validating the creation of standardized organizational security groups:

![Active Directory Role Based Security Groups](ADUC_groups.jpg)

#### 🛠️ Security Engineering & DACL Refinement
1. **Security Group Provisioning:** Generated explicit global security objects (`SG-Finance`, `SG-Marketing`, `SG-HR`) within the corporate domain root to act as logical permission boundaries.
2. **Identity-to-Role Mapping:** Populated the newly engineered security containers with the automated user profiles generated during pipeline ingestion (e.g., nesting Marcus Vance directly inside `SG-Finance`).
3. **Inheritance Disruption:** Structural parent-to-child permission inheritance was explicitly broken at the departmental directory root (`Company_Shares\Finance_Data`). This action severed standard broad access permissions cascading from higher-level file volumes.
4. **DACL Hardening:** Completely purged the generic system-wide `Users` principal string from the security control table. Explicit **Modify, Read & Execute, List Folder Contents, and Write** authorization was injected exclusively for the designated security group (`SG-Finance`).

Below is the hardened Advanced Security configuration window, illustrating broken inheritance and explicit group containment:

![Advanced NTFS File Share Security Boundaries](ntfs_permissions.jpg)

-----

Microsoft 365 Hybrid Identity Infrastructure Lab
A comprehensive, production-grade deployment log detailing the architecture, implementation steps, security mitigations, and validation of a hybrid identity sandbox environment linking an on-premises Windows Server directory to Microsoft Entra ID.

🏢 Environment Architecture Overview
This enterprise simulation bridges a local on-premises network domain controller with a cloud-native tenant space to test hybrid directory operations, automated synchronization workflows, and bi-directional identity properties.

On-Premises Directory Forest: NextTechX.local

Cloud Tenant Space: NextTechX Lab (NEXTTECHXLAB.onmicrosoft.com)

Deployment Platform: Windows Server 2022 Datacenter running inside an isolated Hyper-V virtual environment.

🛠️ Phase 1: Infrastructure Preparation & Core Identity Provisioning
Before configuring directory synchronization tools, the underlying network interfaces and cloud administration spaces required baseline alignment to handle enterprise-level cloud communications.

1. External DNS Resolution and Local Loopback Alignment
Technical Objective: Establish stable public internet routing paths for cloud endpoint registration while maintaining localized Active Directory Domain Services (AD DS) name resolution.

The Challenge: Initial lookups out to public endpoints within the virtual machine failed with DNS_PROBE_FINISHED_BAD_CONFIG errors because the internal interface was isolated from public forwarders while maintaining internal-only name pointers.

Engineering Resolution: The IPv4 configuration on the primary network adapter was systematically modified to balance both lookup requirements:

IP Address assignment managed dynamically via local DHCP routing paths.

Preferred DNS Server pointed directly to the local loopback address (127.0.0.1). This forces the server to look internally first for Active Directory service locator records (SRV), domain controllers, and global catalogs.

Alternate DNS Server explicitly set to Google's public routing interface (8.8.8.8) to capture and resolve outbound public traffic safely.

Verification Command:

DOS
ipconfig /flushdns
* **Documentation Reference:**
  ```markdown
![Network IPv4 Interface Properties Setup](IPv4.jpg)
🔐 Phase 2: Administrative Elevation & Portal Workspace Optimization
2. Tenant Administration RBAC Elevation
Technical Objective: Provision an administrative identity with sufficient security permissions to schema-write, register synchronization agents, and manage tenant objects.

The Error Encountered: Attempting to perform early workspace enrollment resulted in an explicit security block: "You don't have access to this. Your account does not have permission to view or manage this page."

Root Cause Analysis: The active account clearing the initial multi-factor authentication handshake lacked directory-level management rights. Authentic hybrid sync attachment requires a security context with tenant-wide orchestration capabilities.

Engineering Resolution: Accessed the directory control pane using the fallback bootstrap administrator profile and updated the user role allocation matrix. The target identity account was granted explicit directory security visibility.

Assigned Security Profile: Global Administrator role mapped to wlachdaniel@nexttechxlab.onmicrosoft.com.

Documentation Reference:


### 3. Modern Browser Core Upgrades for Cloud Management
* **Technical Objective:** Ensure the server host's web view engines safely support current OAuth 2.0 frames, JavaScript rendering trees, and modern web application interfaces utilized by the Entra ID ecosystem.
* **The Challenge:** The stock version of Microsoft Edge native to fresh Windows Server 2022 media packages (frequently Version 86 or earlier) consistently threw performance warnings and failed to correctly load complex elements within cloud portal interfaces.
* **Engineering Resolution:** Executed a manual browser compilation update across the host node, elevating the installation profile to a current Chromium architecture framework to guarantee smooth communication paths.
* **Documentation Reference:**
  ```markdown
![Outdated Browser Warning](msedge_update.jpg)
![Browser Infrastructure Successfully Patched](msedge_update_done.jpg)



     
     


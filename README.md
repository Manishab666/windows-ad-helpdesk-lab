# Windows Active Directory Help Desk Lab

**Hands-on Windows Server / Active Directory home lab demonstrating AD DS, Organizational Units, Group Policy, NTFS permissions, and Level 1–2 help desk workflows (onboarding, offboarding, account lockouts, login troubleshooting).**

![Windows Server](https://img.shields.io/badge/Windows-Server-0078D4?style=flat-square&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active-Directory-0078D4?style=flat-square)
![Group Policy](https://img.shields.io/badge/Group-Policy-0078D4?style=flat-square)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white)

> **Note:** This is a personal home lab built for skills practice and interview demonstration — not a production or client environment.

---

## Overview

This repository documents a self-built Windows domain lab used to practice the Active Directory administration and desktop support tasks I handle day to day as a Desktop Support Engineer: creating and organizing users, applying Group Policy, managing NTFS/share permissions, and troubleshooting the login and access issues that generate the majority of Level 1–2 help desk tickets.

## Lab Environment

| Component | Details |
|---|---|
| Hypervisor | VirtualBox / Hyper-V |
| Domain Controller | Windows Server 2022 (Evaluation) — `DC01` |
| Client | Windows 11 (Evaluation) — `WKS01` |
| Domain | `lab.local` |
| Roles Installed | AD DS, DNS |

## Objectives

- Stand up a working Active Directory domain from a clean Windows Server install
- Build an OU structure that mirrors a small company (departments, staff, computers)
- Apply and troubleshoot Group Policy
- Configure NTFS and shared-folder permissions for department-based access
- Practice and document common help desk scenarios end to end

## Folder Structure

```
windows-ad-helpdesk-lab/
├── README.md
├── docs/
│   ├── lab-setup.md              # Step-by-step: AD DS install, promotion, DNS config
│   ├── network-diagram.png
│   └── screenshots/
│       ├── 01-ad-users-and-computers.png
│       ├── 02-ou-structure.png
│       ├── 03-group-policy-result.png
│       ├── 04-ntfs-permissions.png
│       ├── 05-domain-join.png
│       └── 06-gpresult-output.png
├── scripts/
│   ├── New-ADUserOnboarding.ps1
│   ├── Reset-ADUserPassword.ps1
│   └── Unlock-ADUserAccount.ps1
└── scenarios/
    ├── 01-employee-onboarding.md
    ├── 02-employee-offboarding.md
    ├── 03-account-lockout-login-troubleshooting.md
    ├── 04-shared-drive-permission-issue.md
    └── 05-group-policy-not-applying.md
```

## Scenarios Demonstrated

1. **Employee Onboarding** — Create AD user in the correct OU, add to department security group, verify home-drive mapping applies via GPO.
2. **Employee Offboarding** — Disable account, move to a "Disabled Users" OU, remove group memberships, document the change.
3. **Account Lockout / Login Troubleshooting** — Identify a locked account via Event Viewer security logs, unlock it (ADUC and PowerShell), confirm root cause.
4. **Shared Drive Permission Issue** — Diagnose "Access Denied" on a department share by checking both NTFS and share-level permissions and AD group membership.
5. **Group Policy Not Applying** — Use `gpresult /r` and `gpupdate /force` to confirm OU linkage and policy scope, then resolve.

Each scenario is documented in `scenarios/` using: **Problem → Diagnostic Steps → Commands Used → Root Cause → Resolution → Verification.**

## Skills Demonstrated

- Active Directory Domain Services installation and configuration
- OU design and Group Policy application/troubleshooting
- NTFS and shared-folder permission management
- DNS fundamentals in a domain environment
- Domain-joining Windows clients
- PowerShell for AD administration (`New-ADUser`, `Set-ADAccountPassword`, `Unlock-ADAccount`)
- Help desk documentation methodology

## Screenshots to Include

- Active Directory Users and Computers showing the OU tree
- A configured Group Policy Object and its settings
- `gpresult /r` output confirming policy application
- NTFS/share permissions dialog for the test share
- Successful domain join confirmation on the client
- `ipconfig /all` on the domain-joined client
- Event Viewer entry for an account lockout

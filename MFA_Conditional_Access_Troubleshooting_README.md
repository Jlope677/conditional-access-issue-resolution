# 🔐 MFA Exclusion Group & Conditional Access Troubleshooting (Microsoft Entra ID)

## 📌 Overview
This lab documents a real-world **Microsoft Entra ID (Azure AD)** troubleshooting scenario involving **MFA exclusion groups**, **Conditional Access policies**, and **location-based access controls**.

The issue was caused by **incorrect group membership** for a remote user and was resolved by aligning the account with the correct security policies.

---

## 🧠 Scenario Summary
An account (`hr.business@maquoketacarecenter.com`) was added to an **MFA Exclusion Group**, which allows users to sign in **without multi-factor authentication**.

This group is intended **only for on-site facility users**.

When the user attempted to sign in **remotely**, they received the following error:

> **“You cannot access this right now. Your sign-in was successful but does not meet the criteria to access this resource.”**

---

## 🛠️ Environment & Tools
- Microsoft Entra ID (Azure AD)
- Security Groups
- Conditional Access Policies
- Named Locations
- Sign-in Logs
- Microsoft 365 / Outlook Web

---

## 👥 MFA Exclusion Group Purpose
**Group Name:** `MFA_Exclusion_Group`

- Group Type: Security  
- Membership Type: Assigned  
- Intended Use:
  - On-site / facility-based accounts only
  - Allows sign-in without MFA when physically at the facility

⚠️ **Remote users should not be members of this group**

### 📸 Screenshot – MFA Exclusion Group Overview
_Add screenshot here_

images/mfa-exclusion-group-overview.png

---

## 👤 User Membership Review
The user `hr.business` was initially added to the MFA exclusion group.

This caused a conflict because:
- The user was working remotely
- The group is restricted by location-based Conditional Access policies

### 📸 Screenshot – Group Members
_Add screenshot here_

images/mfa-exclusion-group-members.png

---

## ❌ Sign-In Error Observed
The user received the following error message during login:

> **You cannot access this right now**

### 📸 Screenshot – Access Error Message
_Add screenshot here_

images/access-block-error.png

---

## 🔍 Conditional Access Policy Analysis
**Policy Name:** `CA101: Block Accounts Outside Named Locations`

- Grant Control: **Block**
- Result: **Failure**
- Condition: User outside approved facility locations

### 📸 Screenshot – Conditional Access Policies
_Add screenshot here_

images/conditional-access-policies.png

---

## 📊 Sign-In Log Review
Sign-in logs confirmed:
- Authentication successful
- Conditional Access failed
- Location outside named locations

### 📸 Screenshot – Sign-In Logs
_Add screenshot here_

images/sign-in-logs.png

---

## 🧩 Root Cause
A remote user was mistakenly added to an **on-site–only MFA exclusion group**, causing Conditional Access to block the sign-in.

---

## ✅ Resolution
### 🔧 Corrective Action
- Removed the user from the `MFA_Exclusion_Group`
- Allowed standard MFA and Conditional Access policies to apply

### 🎯 Result
- User signed in successfully
- Security posture maintained

### 📸 Screenshot – User Removed from Group
_Add screenshot here_

images/user-removed-from-group.png

---

## 📝 What I Learned
- MFA exclusion does not override Conditional Access
- Group membership must align with user role and location
- Removing access can be the correct secure fix
- Sign-in logs are essential for IAM troubleshooting

---

## 📁 Suggested Repo Structure
MFA-Conditional-Access-Troubleshooting/
│
├── README.md
└── images/

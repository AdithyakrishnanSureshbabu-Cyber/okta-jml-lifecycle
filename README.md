# Okta JML Lifecycle Automation

## Overview

I built an automated Joiner-Mover-Leaver identity lifecycle in a free Okta Integrator environment, modelled on a fictional organisation, Meridian Trust Bank.

The access model is group-based rather than user-based. Applications are assigned to groups, and users are automatically placed into the correct groups based on profile attributes such as department.

The project demonstrates how access can be granted, changed, and removed as a user's role changes without manually assigning applications to each individual user.

The most important part of the project was the Mover lifecycle. By changing one department attribute from Lending to Payments, the user's old application access was removed and new access was granted automatically.

---

## What This Project Demonstrates

- Role-Based Access Control using groups
- Group-based application assignment
- Attribute-driven group rules
- Joiner-Mover-Leaver lifecycle management
- Automated provisioning and deprovisioning
- Prevention of privilege creep
- MFA enforcement using Okta Verify
- Password policy hardening
- Least-privilege delegated administration
- Identity lifecycle evidence and audit awareness

---

## Architecture and Access Model

The environment was designed around the principle that applications are assigned to groups rather than directly to users.

### Groups

- Dept-Lending
- Dept-Payments
- All-Staff
- Admins-Helpdesk

### Applications

- OriginateCloud
- PaySuite
- Meridian Intranet

### Application Assignments

- Meridian Intranet → All-Staff
- OriginateCloud → Dept-Lending
- PaySuite → Dept-Payments

This means a user's access is determined by their group membership rather than by manual application assignment.

---

## Attribute-Driven Access

I created department-based Okta group rules.

### Lending Rule

If:

`Department = Lending`

Then:

`Assign user to Dept-Lending`

### Payments Rule

If:

`Department = Payments`

Then:

`Assign user to Dept-Payments`

The rules were activated so that group membership changes automatically when the user profile changes.

---

## The Lifecycle, Evidenced

### Joiner

A new user, Priya Sharma, was created and assigned to the Lending department.

Because her department attribute matched the Lending group rule, she received access to OriginateCloud without the application being manually assigned to her.

[View Joiner Evidence](evidence/01-joiner)

---

### Mover

Priya's department was changed from Lending to Payments.

After the attribute change:

- Lending access was removed
- Payments access was granted
- OriginateCloud disappeared
- PaySuite became available

This demonstrated automated role-based access reassignment and helped prevent privilege creep.

[View Mover Evidence](evidence/02-mover)

---

### Leaver

Priya's account was deactivated to simulate employee offboarding.

After deactivation:

- the account became inactive
- normal sign-in was no longer available
- application access was removed
- the identity remained available for audit history

[View Leaver Evidence](evidence/03-leaver)

---

## Identity Security Hardening

The Okta environment was further strengthened through identity security controls.

### MFA Enforcement

Okta Verify was configured as a required authenticator rather than optional.

### Password Policy

The password policy was strengthened to enforce stronger authentication requirements.

### Least-Privilege Administration

A test Help Desk Administrator role was assigned instead of granting full Super Administrator privileges.

This demonstrated role-scoped administration and least privilege.

[View Hardening Evidence](evidence/04-hardening)

---

## Project Documentation

- [JML Runbook](runbook.md)
- [Project Report](Okta_JML_Project_Report.pdf)

The report provides a concise evidence-led walkthrough of the project.

The runbook documents how the Joiner, Mover, Leaver, authentication, and administrative processes operate.

---

## Lab vs Production

This project was completed in a free Okta Integrator environment using a fictional banking scenario.

Bookmark applications were used as stand-ins for real enterprise applications.

In a production environment:

- user identity attributes would normally come from an HR system
- real applications would typically use SAML or OIDC
- SCIM could be used for downstream provisioning and deprovisioning
- activation flows would replace admin-set test passwords
- production audit logs would be retained for monitoring and compliance

The access automation, group rules, authentication policies, and administrative role configuration were implemented directly in Okta.

---

## Skills Demonstrated

- Identity and Access Management
- Okta Administration
- Joiner-Mover-Leaver Lifecycle
- Role-Based Access Control
- Group-Based Access Control
- Attribute-Driven Access
- Provisioning
- Deprovisioning
- Least Privilege
- MFA Enforcement
- Password Policy Management
- Delegated Administration
- Identity Governance
- Audit Evidence Awareness

---

## Disclaimer

This project was completed in a free Okta Integrator environment using a fictional organisation for training and portfolio purposes.

No real customer, employee, or production organisation data was used.

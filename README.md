# Okta JML Lifecycle Automation

## Overview

I built an automated Joiner-Mover-Leaver identity lifecycle in a free Okta Integrator environment, modelled on a fictional organisation, Meridian Trust Bank.

The access model is group-based rather than user-based. Applications are assigned to groups, and users are placed into the correct groups based on profile attributes such as department.

This project demonstrates how access can be granted, changed, and removed as a user's role changes without manually assigning applications to each individual user.

The key moment in the project was the Mover lifecycle. By changing one department attribute from Lending to Payments, the user's old access was removed and new access was granted automatically.

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

## Access Model

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

This means a user's application access is determined by group membership rather than individual assignment.

---

## Attribute-Driven Group Rules

I created department-based group rules in Okta.

### Lending Rule

If:

`Department = Lending`

Then:

`Assign to Dept-Lending`

### Payments Rule

If:

`Department = Payments`

Then:

`Assign to Dept-Payments`

These rules were activated so group membership could change automatically when a user's department changed.

---

## Joiner Lifecycle

A new user, Priya Sharma, was created and assigned to the Lending department.

Because her department matched the Lending group rule, she received access to OriginateCloud through group membership rather than a direct application assignment.

Evidence of the Joiner process is included in the project report.

---

## Mover Lifecycle

Priya's department was changed from Lending to Payments.

After the attribute change:

- Lending access was removed
- Payments access was granted
- OriginateCloud was removed
- PaySuite became available

This demonstrated automated access reassignment and helped prevent privilege creep.

Evidence of the Mover process is included in the project report.

---

## Leaver Lifecycle

Priya's account was deactivated to simulate employee offboarding.

After deactivation:

- normal sign-in was no longer available
- active access was removed
- the identity remained available for audit history

Evidence of the Leaver process is included in the project report.

---

## Identity Security Hardening

The Okta environment was further strengthened through:

### MFA Enforcement

Okta Verify was configured as a required authenticator.

### Password Policy

The default password policy was strengthened to enforce stronger authentication requirements.

### Least-Privilege Administration

A Help Desk Administrator role was assigned instead of full Super Administrator privileges.

Evidence of these hardening controls is included in the project report.

---

## Project Documentation

- [JML Runbook](runbook.md)
- [Project Report with Evidence](Okta_JML_Project_Report.pdf)

The project report contains the screenshot evidence for:

- group creation
- application configuration
- group-based assignments
- group rules
- Joiner lifecycle
- Mover lifecycle
- Leaver lifecycle
- MFA configuration
- password policy hardening
- delegated Help Desk administration

---

## Lab vs Production

This project was completed in a free Okta Integrator environment using a fictional banking scenario.

Bookmark applications were used as stand-ins for production applications.

In a production environment:

- identity attributes would normally come from an authoritative HR system
- real applications would typically use SAML or OIDC
- SCIM could be used for downstream provisioning and deprovisioning
- activation flows would replace admin-set test passwords
- audit logs would normally be retained for monitoring and compliance

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

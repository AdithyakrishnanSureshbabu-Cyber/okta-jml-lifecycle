# Identity Lifecycle Runbook: Meridian Trust Bank (Okta)

## Purpose

This runbook documents the Joiner, Mover and Leaver lifecycle implemented in the Meridian Trust Bank Okta lab.

The access model is based on group-based application assignment, attribute-driven membership, and least-privilege administration.

---

## Design Principles

### Group-Based Assignment

Applications are assigned to groups rather than directly to individual users.

This makes access management more scalable and allows access to change when group membership changes.

### Attribute-Driven Membership

Group membership is determined by profile attributes such as department.

Example:

`Department = Lending`

assigns the user to:

`Dept-Lending`

### Least-Privilege Administration

Administrative users receive only the permissions required for their role.

Helpdesk users are given a scoped Help Desk Administrator role instead of full Super Administrator privileges.

---

## Joiner

### Trigger

A new employee joins Meridian Trust Bank.

### Manual Step

An administrator creates the user in Okta and sets the required identity attributes.

Example:

- User: Priya Sharma
- Department: Lending

### Automated Actions

After the Department attribute is saved:

1. Okta evaluates the active group rules.
2. The user is added to the correct department group.
3. The user receives the applications assigned to that group.

Example:

`Department = Lending`

results in:

`Dept-Lending`

which provides:

`OriginateCloud`

### Evidence

Evidence is included in the project report and may include:

- user profile
- group membership
- end-user dashboard
- relevant lifecycle screenshots

---

## Mover

### Trigger

An employee transfers to another department.

Example:

Priya Sharma moves from Lending to Payments.

### Manual Step

The Department attribute is changed from:

`Lending`

to:

`Payments`

### Automated Actions

After the attribute change:

1. Okta re-evaluates group membership.
2. The user leaves Dept-Lending.
3. Lending-specific access is removed.
4. The user joins Dept-Payments.
5. Payments-specific access is granted.

### Expected Outcome

OriginateCloud is removed and PaySuite becomes available.

This helps prevent privilege creep.

### Evidence

Evidence is included in the project report and may include:

- updated user profile
- updated group membership
- changed application access
- before and after user dashboard screenshots

---

## Leaver

### Trigger

An employee leaves Meridian Trust Bank.

### Manual Step

The administrator selects:

`More Actions → Deactivate`

### Result

After deactivation:

- authentication is blocked
- application access is removed
- the account remains visible for audit history

### Why Deactivate Instead of Delete

Deactivation removes active access while preserving the identity record and historical evidence.

Deletion would remove the audit trail.

### Evidence

Evidence is included in the project report and may include:

- deactivation confirmation
- Deactivated account status
- sign-in failure evidence

---

## Authentication Policy

### MFA

Okta Verify is configured as a required authenticator.

This reduces reliance on password-only authentication.

### Password Policy

The password policy was strengthened using controls including:

- minimum password length
- uppercase characters
- lowercase characters
- numbers
- restricted/common password protection
- account lockout controls

Routine password expiry was not used as the primary security control.

---

## Administrative Model

### Super Administrator

The main lab administrator retains Super Administrator access.

This role provides unrestricted control of the Okta environment and should be tightly restricted in production.

### Help Desk Administrator

A test user was assigned the Help Desk Administrator role.

The user can perform limited support functions without unrestricted access to:

- group rules
- application configuration
- security policies
- high-risk administrative settings

This demonstrates least-privilege administration.

---

## Automated, Manual and Lab-Specific Activities

| Process | Automated | Manual | Lab Shortcut |
|---|---|---|---|
| Joiner | Group membership and app access | User creation and department entry | Admin-set password |
| Mover | Group and app access changes | Department attribute update | Attribute changed manually |
| Leaver | Access removed after deactivation | Administrator selects Deactivate | Test identity |
| MFA | Policy enforcement | Initial configuration | Test enrollment |
| Applications | Group-based assignment | Initial group-to-app mapping | Bookmark Apps |
| Admin Access | Role-scoped permissions | Admin role assignment | Test helpdesk account |

---

## Lab Shortcuts vs Production

### Admin-Set Passwords

#### Lab

Passwords were set manually because test users used fictional email addresses.

#### Production

Users would normally follow secure activation flows.

### Bookmark Applications

#### Lab

OriginateCloud, PaySuite and Meridian Intranet were configured as Bookmark Apps.

#### Production

Real applications would normally use protocols such as:

- SAML
- OIDC
- SCIM

where supported.

### Identity Attributes

#### Lab

Department attributes were entered manually.

#### Production

Identity attributes would normally originate from an authoritative HR system.

HR events such as hiring, role changes, and termination would drive the lifecycle automatically.

### Audit Evidence

#### Lab

Screenshots were captured as evidence.

#### Production

Okta System Log events would normally be retained and potentially integrated with SIEM or governance tooling.

---

## Operational Summary

### Joiner

Create user → Set department → Group calculated → Access granted

### Mover

Change department → Old group removed → Old access revoked → New group added → New access granted

### Leaver

Deactivate user → Authentication blocked → Access removed → Audit record retained

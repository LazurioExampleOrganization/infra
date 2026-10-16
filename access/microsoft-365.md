# Microsoft 365 tenant of Lazurio Example Organization

First recorded: 2026-10-16

## Purpose and readiness

This is the Organization's own Microsoft 365 Business Premium trial tenant.
It is intended as the first canary for the Microsoft 365 company app under
DEV-6626, Lazurio root decision 0162 (addendum 2026-10-14) and decision 0204.
The shared IT procedure is maintained in
[`HumanAndMachines/Lazurio`, `manual/integrations/microsoft-365.md`](https://github.com/HumanAndMachines/Lazurio/blob/main/manual/integrations/microsoft-365.md).

**Provisioning is incomplete. Recurring billing is still On.** The tenant is
not ready for integration testing. The next step is to resolve
[infra issue #5](https://github.com/LazurioExampleOrganization/infra/issues/5)
and verify renewal is Off while service remains active. User and SharePoint
setup must wait for that gate.

## State

Verified 2026-10-16. Source: the live Microsoft 365 signup flow and Microsoft
365 admin center, Billing → Your products → Microsoft 365 Business Premium.
Unverified items are explicitly marked below.

| Item | Observed state |
| --- | --- |
| Organization display name | Lazurio Example Organization |
| Provisioned sign-in domain | `lazurioexampleorganization.onmicrosoft.com` |
| Tenant created | 2026-10-16 |
| Subscription | Microsoft 365 Business Premium, active free trial |
| Trial seats | Microsoft provisioned 25 temporary seats; one is assigned |
| Planned paid conversion | One license, yearly renewal; no paid conversion was started manually |
| Recurring billing | **On — unresolved blocker; not Off** |
| Trial end | Product overview shows `15/11/2026`; renewal pane describes `16 November 2026`. The cutoff needs clarification before this record can report one authoritative date |
| Tenant ID | Not yet verified in Microsoft Entra Overview |
| Primary domain | The provisioned sign-in domain is above; primary-domain status has not yet been independently checked |
| Custom domain | None added during provisioning |
| Security defaults | Not changed; the enabled state has not yet been read back |
| Conditional Access | No policy was created or changed during provisioning; existing tenant policy inventory has not yet been checked |

The signup account was assigned the trial license automatically. The final
configuration uses one licensed standard user and an unlicensed administrator;
that reassignment has not happened yet. Trial capacity is not an instruction
to purchase or assign 25 paid licenses.

## Renewal blocker

Selecting **Edit recurring billing → Cancel on expiration** opens Microsoft's
cancellation flow. Its final review says the effective cancellation date is
**16 October 2026**, with access ending that day, despite the preceding pane
describing expiration on **16 November 2026**. The final confirmation was not
selected. The subscription was kept active, and readback still shows
recurring billing On.

Microsoft's
[documented recurring-billing behavior](https://learn.microsoft.com/en-us/microsoft-365/commerce/subscriptions/renew-your-subscription?view=o365-worldwide)
keeps a subscription active until expiry when renewal is disabled. Obtain a
supported way to achieve that behavior and verify the result before
continuing. Do not use immediate cancellation as a workaround.

## Accounts

Both intended identities are fictional and Example-only, not accounts for
real people.

| Account | Intended role and license | Current state |
| --- | --- | --- |
| Example Admin — `admin@lazurioexampleorganization.onmicrosoft.com` | Global Administrator; no Business Premium license needed for administration | Account created and admin-center sign-in verified. Display name still needs to be changed to Example Admin; the automatically assigned trial license still needs to be removed after the renewal gate |
| Sam Taylor — `sam.taylor@lazurioexampleorganization.onmicrosoft.com` | Standard user with the single Business Premium license | Not created yet. Require a password change at first sign-in, then verify mailbox provisioning |

The Owner performed administrator authentication and the MFA steps. The
authentication-method inventory has not been inspected; do not treat
successful sign-in as proof that Security defaults is enabled.

## SharePoint fixture

Not created yet. The intended fixture is a team site named **Example**, with
`Documents/Zakázky/ukazka.txt` containing:

> Ukázkový dokument Lazurio Example Organization.

Record the actual site URL and verify the file can be opened after the
renewal gate. Do not invent a site URL from the tenant domain.

## Ownership and credential custody

Billing and recovery belong to the Organization Owner. Actual payment,
contact and recovery details stay outside this public repository.

The Owner maintains credentials in the Owner's password manager under these
entry titles; this record does not inspect or attest to their contents:

- `LazurioExampleOrganization – M365 Example Admin`
- `LazurioExampleOrganization – Sam Taylor` (planned)

Passwords, MFA enrollment material, verification codes, personal contact
details, card details, tokens and session data must never enter Git or issues.

## Not yet

- Complete the renewal gate, administrator display name and license
  reassignment, Sam Taylor, mailbox and SharePoint fixture, then verify the
  Tenant ID, primary domain, Security defaults and authoritative trial end.
- The Entra company app is a separate next step for IT, following the shared
  Microsoft 365 procedure linked above. No app registration, application
  consent or external connector was created in this task.
- `settings.integrations.microsoft365` remains unset. Add it only after the
  company app exists and compatible readers have been released.

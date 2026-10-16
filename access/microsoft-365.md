# Microsoft 365 tenant of Lazurio Example Organization

First recorded: 2026-10-16

## Purpose and readiness

This is the Organization's own Microsoft 365 Business Premium trial tenant.
It is intended as the first canary for the Microsoft 365 company app under
DEV-6626, Lazurio root decision 0162 (addendum 2026-10-14) and decision 0204.
The shared IT procedure is maintained in
[`HumanAndMachines/Lazurio`, `manual/integrations/microsoft-365.md`](https://github.com/HumanAndMachines/Lazurio/blob/main/manual/integrations/microsoft-365.md).

**Provisioning is incomplete. Recurring billing is still On.** Renewal is
tracked in [infra issue #5](https://github.com/LazurioExampleOrganization/infra/issues/5).
On 2026-10-16, the Organization Admin explicitly allowed user and SharePoint
setup to continue while Microsoft support resolves renewal. Verify each
remaining setup item below before treating the tenant as ready for testing.

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
| Trial seats | Microsoft provisioned 25 temporary seats; the administrator's assignment has been removed, and Sam's single assignment is being prepared |
| Planned paid conversion | One license, yearly renewal; no paid conversion was started manually |
| Recurring billing | **On — unresolved blocker; not Off** |
| Trial end | Product overview shows `15/11/2026`; renewal pane describes `16 November 2026`. The cutoff needs clarification before this record can report one authoritative date |
| Tenant ID | Not yet verified in Microsoft Entra Overview |
| Primary domain | The provisioned sign-in domain is above; primary-domain status has not yet been independently checked |
| Custom domain | None added during provisioning |
| Security defaults | Not changed; the enabled state has not yet been read back |
| Conditional Access | No policy was created or changed during provisioning; existing tenant policy inventory has not yet been checked |

The signup account was assigned the trial license automatically; that license
has now been removed. The final configuration uses one licensed standard user
and an unlicensed administrator. Trial capacity is not an instruction to
purchase or assign 25 paid licenses.

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
supported way to achieve that behavior and verify the result before marking
the billing issue resolved. Do not use immediate cancellation as a workaround.

## Microsoft support follow-up

On 2026-10-16, the Organization Admin authorized sending the reproduction to
Microsoft. The Admin subsequently waived the ordering gate and authorized
finishing tenant setup while renewal is being resolved. Microsoft 365
admin center confirmed service request **2610161420001741**, status **Open**,
severity **C**, awaiting assignment when first recorded.

The request explicitly asks Microsoft to turn recurring billing Off while
preserving active trial access, without an immediate cancellation, paid
conversion or additional paid licenses. It also asks Microsoft to clarify
the conflicting expiry dates. Submission is not evidence that renewal has
been disabled: the last verified billing state remains **On**.

The Owner can find the case in Microsoft 365 admin center → Help & support →
Service requests. Correspondence and real contact details stay in Microsoft,
outside this public repository. The billing acceptance check is a live
readback of recurring billing **Off**, active trial service and the
authoritative end date. If Off has not been verified by **2026-11-09**, notify
the Owner so the Owner can decide on cancellation before the paid conversion.
That deadline does not authorize automatic or immediate cancellation.

## Accounts

Both intended identities are fictional and Example-only, not accounts for
real people.

| Account | Intended role and license | Current state |
| --- | --- | --- |
| Example Admin — `admin@lazurioexampleorganization.onmicrosoft.com` | Global Administrator; unlicensed | Display name and Global Administrator role verified. License removal saved; the admin center reports zero assigned licenses for this account |
| Sam Taylor — `sam.taylor@lazurioexampleorganization.onmicrosoft.com` | Standard user with the single Business Premium license | Wizard configured with Czech Republic usage location, Business Premium and no administration access. Password change at first sign-in is enabled. Waiting for the human to enter the password and finish creation before mailbox verification |

The Owner performed administrator authentication and the MFA steps. The
authentication-method inventory has not been inspected; do not treat
successful sign-in as proof that Security defaults is enabled.

## SharePoint fixture

Not created yet. The intended fixture is a team site named **Example**, with
`Documents/Zakázky/ukazka.txt` containing:

> Ukázkový dokument Lazurio Example Organization.

Record the actual site URL and verify the file can be opened. Do not invent a
site URL from the tenant domain.

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

- Complete the administrator display name and license
  reassignment, Sam Taylor, mailbox and SharePoint fixture, then verify the
  Tenant ID, primary domain, Security defaults and authoritative trial end.
- The Entra company app is a separate next step for IT, following the shared
  Microsoft 365 procedure linked above. No app registration, application
  consent or external connector was created in this task.
- `settings.integrations.microsoft365` remains unset. Add it only after the
  company app exists and compatible readers have been released.

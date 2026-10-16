# Microsoft 365 tenant of Lazurio Example Organization

First recorded: 2026-10-16

## Purpose and readiness

This is the Organization's own Microsoft 365 Business Premium trial tenant.
It is intended as the first canary for the Microsoft 365 company app under
DEV-6626, Lazurio root decision 0162 (addendum 2026-10-14) and decision 0204.
The shared IT procedure is maintained in
[`HumanAndMachines/Lazurio`, `manual/integrations/microsoft-365.md`](https://github.com/HumanAndMachines/Lazurio/blob/main/manual/integrations/microsoft-365.md).

**The user, mailbox and SharePoint fixture are provisioned. Recurring billing
is still On.** Renewal is
tracked in [infra issue #5](https://github.com/LazurioExampleOrganization/infra/issues/5).
On 2026-10-16, the Organization Admin explicitly allowed user and SharePoint
setup to continue while Microsoft support resolves renewal. Verify each
remaining acceptance item below before treating the billing issue as closed.

## State

Verified 2026-10-16. Source: the live Microsoft 365 signup flow and Microsoft
365 admin center, Billing → Your products → Microsoft 365 Business Premium,
and Microsoft Entra admin center → Overview → Properties → Manage security
defaults.
Unverified items are explicitly marked below.

| Item | Observed state |
| --- | --- |
| Organization display name | Lazurio Example Organization |
| Tenant country/region | Czechia |
| Provisioned sign-in domain | `lazurioexampleorganization.onmicrosoft.com` |
| Tenant created | 2026-10-16 |
| Subscription | Microsoft 365 Business Premium, active free trial |
| Trial seats | Microsoft provisioned 25 temporary seats; Sam has one assignment, Example Admin has none, and 24 seats remain available |
| Planned paid conversion | One license, yearly renewal; no paid conversion was started manually |
| Recurring billing | **On — unresolved blocker; not Off** |
| Trial end | Product overview shows `15/11/2026`; renewal pane describes `16 November 2026`. The cutoff needs clarification before this record can report one authoritative date |
| Tenant ID | `9755f325-aab4-4294-8232-88dcfefacb96`, verified in Entra Home and Overview |
| Primary domain | `lazurioexampleorganization.onmicrosoft.com`, verified in Entra Home and Overview |
| Custom domain | None; Entra Domain names lists only the primary `onmicrosoft.com` domain |
| Security defaults | **Enabled**, read back in Manage security defaults; no change saved |
| Conditional Access | No policy created or changed; Policies shows the empty onboarding view with “Create your first policy” |

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
severity **C**. The case now shows **Agent assigned**. Microsoft's initial
AI-generated guidance asks whether the UI has a true On/Off control and
whether a payment method is attached; it confirms not to complete an
immediate cancellation. The UI only offers Renew / Cancel on expiration,
and a payment method was supplied during signup. An email reply was sent
on 2026-10-16, answering those questions, requesting a billing specialist
and reiterating the prohibition on immediate cancellation, paid conversion
or additional paid licenses. Gmail confirmed the message was sent to the
existing Microsoft support thread. A Microsoft resolution is still required;
no Off state has been verified.

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

Both identities are fictional and Example-only, not accounts for
real people.

| Account | Intended role and license | Current state |
| --- | --- | --- |
| Example Admin — `admin@lazurioexampleorganization.onmicrosoft.com` | Global Administrator; unlicensed | Display name and Global Administrator role verified. License removal saved; the admin center reports zero assigned licenses for this account |
| Sam Taylor — `sam.taylor@lazurioexampleorganization.onmicrosoft.com` | Standard user with the single Business Premium license | Created by the Owner; display name corrected and read back as Sam Taylor. No administrator access. Licenses and apps reports one Business Premium assignment and 24 of 25 seats available. The wizard's first-sign-in password-change requirement was enabled; no first sign-in was performed |

Sam's mailbox is provisioned: Users → Sam Taylor → Mail displays mailbox
storage of 19.55 KB / 100 GB. Mail delivery and a first sign-in were not tested.
Email-app settings were not changed.

The Owner performed administrator authentication and the MFA steps. The
authentication-method inventory has not been inspected. Security defaults
was verified separately in the tenant's Properties pane.

## SharePoint fixture

The private **Example** team site was created on 2026-10-16 using the Standard
team template, Czech site language and Prague time zone. Example Admin is
the group owner. The home page was opened successfully at:

<https://lazurioexampleorganization.sharepoint.com/sites/Example>

Its Documents library contains `Zakázky/ukazka.txt`:

> Ukázkový dokument Lazurio Example Organization.

The folder and file were created through the SharePoint UI. The file was
saved, closed and reopened, and its exact text was read back successfully.
The library's actual path is `/sites/Example/Sdilene dokumenty/`.
Group membership was saved and read back as two members: Example Admin
(Owner) and Sam Taylor (Member). Sam has not yet signed in, so access under
his session has not been tested.

## Ownership and credential custody

Billing and recovery belong to the Organization Owner. Actual payment,
contact and recovery details stay outside this public repository.

The Owner maintains credentials in the Owner's password manager under these
entry titles; this record does not inspect or attest to their contents:

- `LazurioExampleOrganization – M365 Example Admin`
- `LazurioExampleOrganization – Sam Taylor` (entry created in the Owner's personal vault; the Owner confirmed storing its password)

Passwords, MFA enrollment material, verification codes, personal contact
details, card details, tokens and session data must never enter Git or issues.

## Not yet

- Resolve recurring billing and verify the authoritative trial end. A first
  sign-in as Sam (including the required password change and any MFA) and
  mail delivery / file access tests remain human-assisted follow-up checks.
- The Entra company app is a separate next step for IT, following the shared
  Microsoft 365 procedure linked above. No app registration, application
  consent or external connector was created in this task.
- `settings.integrations.microsoft365` remains unset. Add it only after the
  company app exists and compatible readers have been released.

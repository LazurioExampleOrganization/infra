# Microsoft 365 tenant of Lazurio Example Organization

First recorded: 2026-10-16

## Purpose and readiness

This is the Organization's own Microsoft 365 Business Premium trial tenant.
It is intended as the first canary for the Microsoft 365 company app under
DEV-6626, Lazurio root decision 0162 (addendum 2026-10-14) and decision 0204.
The shared IT procedure is maintained in
[`HumanAndMachines/Lazurio`, `manual/integrations/microsoft-365.md`](https://github.com/HumanAndMachines/Lazurio/blob/main/manual/integrations/microsoft-365.md).

**Provisioning and Sam's SharePoint file-read test are complete. Outlook
access remains a readiness blocker after Microsoft support's billing
intervention.** The Owner reports that Microsoft
confirmed no future charges. The admin center still displays **Disabled** and
recurring billing **On**. These are separate observations: neither an expiry
date nor the no-charge assurance proves that Sam can use the services.
The remaining Outlook and renewal checks are tracked in
[infra issue #5](https://github.com/LazurioExampleOrganization/infra/issues/5).

## State

Verified 2026-10-16. Source: the live Microsoft 365 signup flow and Microsoft
365 admin center, Billing → Your products → Microsoft 365 Business Premium,
and Microsoft Entra admin center → Overview → Properties → Manage security
defaults.
Identity, security and license-assignment observations come from provisioning
before the support call. Subscription observations below are from after that
call. Browser service tests are described separately; an assignment is not
proof of an active entitlement. Unverified items are explicitly marked.

| Item | Observed state |
| --- | --- |
| Organization display name | Lazurio Example Organization |
| Tenant country/region | Czechia |
| Provisioned sign-in domain | `lazurioexampleorganization.onmicrosoft.com` |
| Tenant created | 2026-10-16 |
| Subscription | Microsoft 365 Business Premium free trial; the post-support portal status is **Disabled**, with a data-deletion warning |
| Trial seats | Before the support call: 25 temporary seats, one assigned to Sam, none to Example Admin, 24 available. This is an assignment count, not a claim that services remain active |
| Planned paid conversion | The portal still describes one yearly paid license from 2026-11-16; Microsoft support assured the Owner that no future charges would occur. No manual paid conversion was started |
| Recurring billing | The portal still displays **On** after the support call; support reports renewal disabled. An Off readback has not been obtained |
| Trial end | Expiration date **2026-11-15** in the product overview; the portal also describes paid conversion on 2026-11-16. An authoritative cutoff timestamp/time zone has not been provided |
| Tenant ID | `9755f325-aab4-4294-8232-88dcfefacb96`, verified in Entra Home and Overview |
| Primary domain | `lazurioexampleorganization.onmicrosoft.com`, verified in Entra Home and Overview |
| Custom domain | None; Entra Domain names lists only the primary `onmicrosoft.com` domain |
| Security defaults | **Enabled**, read back in Manage security defaults; no change saved |
| Conditional Access | No policy created or changed; Policies shows the empty onboarding view with “Create your first policy” |

The signup account was assigned the trial license automatically; that license
has now been removed. The final configuration uses one licensed standard user
and an unlicensed administrator. Trial capacity is not an instruction to
purchase or assign 25 paid licenses.

## Renewal and Microsoft support

Service request **2610161420001741** was opened on 2026-10-16 (severity C).
Before the support call, **Edit recurring billing → Cancel on expiration**
opened a cancellation review with an effective date of 2026-10-16, despite
the preceding pane describing November expiry. That initial attempt was
abandoned without confirmation and the trial remained active.

The Owner subsequently completed a phone and screen-sharing session with
Microsoft support. The Owner reports that support confirmed renewal had
been disabled and there would be no future charges. Microsoft's email of
2026-10-16 at 19:58 Europe/Prague describes the recurring-billing issue as
resolved, says support is proceeding with case closure, and allows reopening
through the admin portal within 14 days. This email does not establish that
the case has already closed; the last checked portal case status was
**Agent assigned**.

After that intervention, the product page displays **Disabled**, a warning
that data will be deleted, recurring billing **On**, expiry **2026-11-15**,
and a conversion description dated **2026-11-16**. Do not describe this as an
active trial or claim an Off readback. The cause of any service failure must
be diagnosed separately; the status alone is not proof of the cause.

The Owner's latest instruction requires approval before any further support
message, public update or billing change. Do not reactivate, cancel, purchase
licenses or start a paid subscription automatically. If future-charge status
still needs clarification by **2026-11-09**, notify the Owner, acknowledge
Microsoft's no-charge assurance and leave any cancellation decision to the
Owner. The support case and its correspondence contain the private contact
details; those details do not belong in this public record.

## Accounts

Both identities are fictional and Example-only, not accounts for
real people.

| Account | Intended role and license | Current state |
| --- | --- | --- |
| Example Admin — `admin@lazurioexampleorganization.onmicrosoft.com` | Global Administrator; unlicensed | Display name and Global Administrator role verified. License removal saved; the admin center reports zero assigned licenses for this account |
| Sam Taylor — `sam.taylor@lazurioexampleorganization.onmicrosoft.com` | Standard user with the single Business Premium license | Created by the Owner; display name corrected and read back as Sam Taylor. No administrator access. Before the support call, Licenses and apps reported one Business Premium assignment and 24 of 25 seats available. The wizard's first-sign-in password-change requirement was enabled. The Owner subsequently completed sign-in; the Microsoft account picker and Microsoft 365 portal show Sam signed in |

Sam's mailbox was provisioned: before the support call, Users → Sam Taylor
→ Mail displayed mailbox storage of 19.55 KB / 100 GB. On 2026-10-16, selecting
the signed-in Sam account and opening Outlook reached **Something went wrong**
instead of an inbox; a refresh repeated the error. Mailbox access has not
passed. After the fresh SharePoint sign-in, a further Outlook attempt remained
on the loading screen instead of reaching an inbox. No diagnostic established
the cause. Mail delivery was not tested. Email-app settings were not changed.

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
(Owner) and Sam Taylor (Member). After the support call the file remained
readable as Example Admin. Sam signed in to Microsoft 365, but SharePoint
retained the administrator session; a test under that session is not evidence
of Sam's access. After the Owner completed Sam's separate site sign-in, the
SharePoint header identified **Sam Taylor**. Under that session,
`Zakázky/ukazka.txt` was opened and the exact text above was read back
successfully on 2026-10-16. No permission change was made to make the test
pass. This verifies browser file access as Sam; Graph access remains a
separate integration test.

## Entra company app

Created and verified 2026-10-16 in Microsoft Entra admin center, signed in as
Example Admin in this tenant. The Organization Admin authorized registration
and tenant-wide admin consent for the following delegated permissions.

| Item | Verified state |
| --- | --- |
| Display name | `Lazurio (Lazurio Example Organization)` |
| Application (client) ID | `e2ad5755-21c1-46db-bfcb-8ba290440414` |
| Directory (tenant) ID | `9755f325-aab4-4294-8232-88dcfefacb96` |
| Supported account types | My organization only (`AzureADMyOrg`, single tenant) |
| Authentication platform | Mobile and desktop applications only |
| Redirect URI | `http://localhost/api/oauth/callback` — the only registered URI |
| Web / SPA platforms | None; Overview reports 0 web, 0 spa, 1 public client |
| Allow public client flows | Disabled (No) |
| Client secrets / certificates / federated credentials | 0 / 0 / 0 |
| Enterprise application: Assignment required | No (Off), retained for this test tenant |
| Enterprise application: Enabled for users to sign in | Yes |

API permissions contains exactly these nine **Microsoft Graph Delegated**
permissions, each read back as **Granted for Lazurio Example Organization**:

- `openid`
- `profile`
- `email`
- `offline_access`
- `User.Read`
- `Mail.ReadWrite`
- `Calendars.ReadWrite`
- `Files.ReadWrite.All`
- `Sites.Read.All`

There are no Application permissions and no `Mail.Send` permission.
Verification used the saved Overview, Authentication (Preview), API permissions,
Certificates & secrets, and Enterprise application Properties pages. Public
client flows remained disabled; no secret or certificate was created.

The Organization has no hosted Environment callback to register yet. Add its
Launchpad callback later using the shared IT runbook. Registration and admin
consent are complete; an OAuth sign-in, token refresh and Graph access through
Lazurio have not been tested by this provisioning task.

## Handoff for integration testing (DEV-6626)

The identifiers are available now; another task does not need to wait for
Tenant ID discovery. Use the tenant and client IDs in this record, Sam's
fictional account and the Example site/file fixture. The app configuration
was published separately in [infra PR #8](https://github.com/LazurioExampleOrganization/infra/pull/8);
this service-verification task has not changed that application or its consent.

A Microsoft browser session is not a Lazurio integration connection. Do not
copy browser cookies, credentials or tokens into T3, Git, issue comments or
handoff prompts. The Owner performs any password/MFA step directly.
`settings.integrations.microsoft365` is still unset; only activate it once
compatible readers are released and the applicable Organization change is
approved. OAuth sign-in, refresh and delegated Graph mail/file access are
separate acceptance tests under the shared runbook. SharePoint discovery and
file-read integration tests can proceed independently of Outlook. Browser
SharePoint access has passed; Graph access has not yet been tested.

On 2026-10-17, the Owner chose to continue with the working SharePoint path
and defer further Microsoft correspondence. Retry Outlook later; delayed
mailbox provisioning is a hypothesis, not a confirmed explanation of the
observed error/loading. Do not mark the mail canary passed until an inbox
opens and the relevant integration checks succeed.

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

- Resolve the post-support service-readiness results and reconcile the portal
  billing state with Microsoft's no-charge assurance. Mail delivery remains
  untested; no test message was sent.
- Connect and test the Entra company app through the shared Microsoft 365
  procedure. No external connector or integration connection was created by
  this app-provisioning task.
- `settings.integrations.microsoft365` remains unset. Add it only after the
  company app exists and compatible readers have been released.

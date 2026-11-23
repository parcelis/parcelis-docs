---
title: Organization Settings
slug: /organization-settings
---
Open **Settings → Organization → General** at `/settings/organization/general` to manage the active organization.
Organization links retain the `/o/<organization-slug>` prefix. The previous organization settings address redirects to General.

Organization administrators can update the organization name, address, phone number, contact email address, and URL slug. Saving a new
slug updates the organization URL; use the new URL for subsequent navigation.

Set **Timezone for lease dates** to the organization's timezone. Existing organizations use UTC until an
administrator selects another timezone. This setting determines the local calendar day for automated lease
activation and expiration. Note timestamps also use this timezone, including daylight saving time.
While the timezone loads, notes remain visible and their timestamps are hidden. If loading fails,
select **Retry** beside **Unable to load note timestamps** to load the timestamps again.

Administrators can also upload or remove separate organization avatars for light and dark themes. Use JPG, PNG,
WebP, or GIF images up to 2 MB. The active organization's avatar appears in the expanded sidebar.

### Organization address

Use the organization address to record the business's own mailing address for organization-level contacts and
correspondence, separate from any individual property's address. Click the address field to open the address
editor, which accepts:

- Address line 1
- Address line 2 (optional)
- City
- State (2-letter abbreviation)
- Postal code

All address fields are optional and can be left blank. Members without administrator access see the saved address
as read-only text.

### Organization contact email

Enter a valid address in **Organization email address (optional)** and select **Update organization** to save the
business's primary contact email. Leave the field blank to remove it. Existing organizations can keep it empty;
members with view-only access see the saved address or **Not provided**.

This contact address does not change the sender or SMTP configuration for outgoing messages. Configure those
separately in [Email Settings](./email-settings.md).

If you can access more than one organization, use the **Organization** selector near the top of the expanded sidebar
to switch workspaces. Properties, tenants, leases, invoices, maintenance, and related operational records are shown
for the selected organization.

### View organization contact information

Under **Settings → Organization → General → Organizations**, select **Contact information** on an
organization row to view its saved email, phone number, and mailing address. The panel is read-only and
available even without permission to edit organization settings. It only shows details for organizations
you can access.

Missing fields show **Not provided**. If no contact details are configured, the panel shows
**No contact information has been provided.** Organization administrators can update these details in
the organization's General settings.

### Currency

**Currency** shows the saved operating currency as a code and name, initially **USD — US Dollar**.
USD is currently the only supported option and is already selected; no selection is required.
Available choices and permission to change currency come from the server. When additional currencies
are supported, eligible owners and administrators can select one and choose **Update organization**.
Members see the saved value read-only.

Once monetary records use the currency, it becomes permanently read-only with an explanation.
Clearing amounts or deleting records does not unlock it. Eligibility is checked again on save;
if another session saves monetary data first, the rejection keeps your entered organization
details available for retry. Failed saves do not activate an unsaved currency selection.
Successful saves refresh the saved currency and monetary amounts. Switching organizations loads
that workspace's currency before showing its monetary screens. If currency loading fails,
select **Retry loading currency** to load it again; monetary screens remain hidden until it succeeds.

Enter unit rates, application income, rent, deposits, invoices, payments, and allocations in major
units of the displayed currency. For USD, enter `12.34` for twelve dollars and thirty-four cents.
Inputs reject excess nonzero decimal places and amounts above the supported storage limit rather
than rounding them. Existing lease and invoice amounts retain their saved record currency.

Currency is independent of browser locale, dates, timezone, addresses, and payment methods.
Parcelis does not perform exchange-rate conversion or mixed-currency billing.

### API tokens

Open **Settings → Organization → API tokens** to manage integration credentials for
the active organization. Organization owners and administrators can manage tokens;
platform administrators can do so without membership. Other members see an access
message instead of token management controls.

Select **Create token**, enter a name, and choose an expiration. The default is
**7 days**; month presets and **Never** are also available. Copy the complete token
from the one-time dialog before closing it. Its secret cannot be retrieved later.

The paginated table shows metadata and Active, Expired, or Revoked status. **Revoke**
asks for confirmation and stops subsequent authentication, while a request already
in progress may finish. Revoked rows remain visible. To rotate, create a replacement,
update the integration, then revoke the old token.

Tokens belong to the organization, independently of their creator, and grant full
access to supported organization REST operations without granular scopes. Read
[API Authentication](../../API%20Reference/api-authentication.md) for access details, Bruno and curl
setup, and troubleshooting.

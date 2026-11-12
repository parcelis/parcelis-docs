---
title: Income Dashboard
slug: /income-dashboard
---
Use **Income** in the sidebar to review rent income across the portfolio.
The dashboard requires both Invoices View and Leases View. Without Leases View, income is
**Unavailable**. If loading your permissions fails, select **Retry**.

The dashboard separates active/notice monthly rent, net payments recorded across all dates, overdue balances,
amounts due today, and future scheduled balances. Invoice totals include ended and archived leases. Voided invoices
are excluded; reversed payments reduce net payments. These are recorded invoice payments, not earned rent revenue
or a monthly cash-flow forecast, and may include deposits and other charges.

An invoice becomes overdue on the calendar day after its due date in the organization's timezone. Invoices due today
are not overdue. Future unpaid invoices are marked **Upcoming**. Date-only due dates keep their entered calendar date.
Only saved invoices appear; leases without saved invoices do not create estimated invoice rows.
In the ungrouped view, these leases display **No saved invoices for this lease**.
Their grouped invoice totals remain zero.
Joint obligations count once. A tenant filter includes only invoices assigned to that tenant; a shared invoice shows
the whole shared obligation rather than a separate amount owed by each co-tenant.

Use the search field to find income records by property, unit, tenant name, or lease status.

The directory loads saved invoices directly. A former recipient can still find their invoice through a tenant-filtered
link even if they no longer belong to the lease. Lease records without current tenants retain their saved invoices.

Select **Filters** to choose **Lease history**: all history (the default), current and scheduled leases, or ended and
archived leases. Use **Invoices** to select non-void invoices (the default), all saved invoices, outstanding invoices,
fully paid invoices, or voided invoices. Select **Apply Filters** to apply your choices. Void invoices remain available
for review but contribute zero to balance and payment summaries. Group totals also exclude void invoices.

Property, unit, lease-history, and invoice filters apply together to the table and invoice summaries. Scheduled monthly
rent represents active/notice leases within the property, unit, and current tenant scope. Invoice status and lease-history
filters do not change scheduled rent. It is not an invoice balance. Search narrows table
rows. **Clear Filters** resets all four filters while keeping search, grouping, and any tenant restriction. Property and
unit selections remain in the page address; lease-history and invoice selections last until the page reloads.

**New Invoice** appears only with Invoices Create permission.

Select **Filters** to narrow income by **Property** and optionally **Unit**, then select **Apply Filters**.
Both default to **All properties** and **All units**. Choosing a property limits the Unit options to that
property. Changing properties resets a selected unit if it belongs to another property. With All properties
selected, units remain grouped under their property so units with the same name stay distinct. Units with
finalized lease history matching the pending filters and tenant scope are listed.

The invoice summaries and both table layouts follow the property and unit selections. A property without
matching records shows an empty state. Selections are saved in the page address as `/income?propertyId=3`
or `/income?propertyId=3&unitId=12`. Existing unit-only links such as `/income?unitId=12` continue to work.
A property/unit combination that does not match shows no income results.

If the page was opened with a `tenantId` restriction, a notice identifies the tenant scope.
**Clear Filters** keeps that restriction and its notice visible.

## Manual Invoices

Select **New Invoice** to add a charge for an existing lease. Choose the property, unit, and lease term; the linked
tenant is filled in automatically. With Invoices Create, you can create an invoice even when
Tenants View is denied: the tenant field displays **Unavailable**, and the invoice uses the lease's
linked tenant. When no tenant is supplied, Parcelis uses the tenant added to the lease earliest,
with the lowest tenant ID breaking ties. For individual billing, only that tenant receives the invoice.
Select **Add item** to choose a configured charge or **Custom item**. A configured
charge fills in its default description, with `{month}` and `{year}` filled from the due date; a custom item lets you
enter its name. You can edit the description for this
invoice. The form shows the subtotal, paid amount, and balance due before the invoice is created. Manage reusable
item names and descriptions in
**Settings → Invoicing**. Saved invoices keep a copy of the item and description as entered.

If you change any field or add a charge line, closing the drawer with **X**, **Cancel**, an outside click, or **Escape**
shows **Your changes will not be saved.** Select **Keep Editing** to retain all entered values, or **Discard** to close
the drawer and clear the form. Pressing **Escape** in the confirmation also keeps your edits. An untouched form, or
one returned to its initial values, closes without a warning.

The drawer stays open while invoice creation is in progress. A successful save closes and clears it; if creation
fails, your values remain available to edit or retry, and closing still requires confirmation.

When creating a manual invoice, an **Already paid** amount is saved as a payment using the selected tenant,
the invoice due date, and payment method **Other**. This also applies to partial payments. Use **Record payment**
when you need to specify the actual payment date and method instead. Existing fully paid invoices with a saved
settlement date and no payment history receive a payment record during upgrade, preserving that date and any saved
payer or method; missing payer and method use the invoice tenant and **Other**. Dates already lost before the
upgrade cannot be recovered automatically.

## Manage an Invoice

Select an invoice identifier to open its details. The property rail groups invoices by property and unit, making it
easy to move between related invoices.

Use **Edit invoice** to change the due date or charge lines. You can add and remove charge lines, but an invoice
always requires at least one line. The edit form shows the existing paid amount and balance so you can review the
effect of the changes before saving. If an increase leaves a previously paid invoice with a balance, its paid
settlement details are cleared; recorded payments and their history remain intact. Edits that leave the invoice fully
paid preserve its settlement details. If a later edit brings the balance back to zero, settlement details are restored
from the latest non-reversed payment. The total cannot be reduced below the amount already paid.

Use **Record payment** to add the first payment, or **Add payment** when the invoice already has a payment. A fully
paid invoice is marked **PAID**; invoices with a remaining balance are shown as open, overdue, or partially paid as
appropriate. Use **Add note** to attach internal notes to the invoice. **Delete** permanently removes an invoice and
its charge lines. Delete is disabled for invoices with payment history, including invoices whose
payments have all been reversed. Hover over **Delete** or move keyboard focus to the button
to see a tooltip explaining why deletion is unavailable. Reversing a payment preserves its history and does not make
the invoice eligible for deletion.

To correct a recorded payment, use **Reverse payment** in the invoice's **Payment activity** section, enter a reason,
and confirm. This action requires invoice deletion permission. The original payment remains visible with the reversal
date, staff member, and reason, and its amount is added back to the outstanding balance. Other payments, including
payments from co-tenants, remain unchanged. Repeating a reversal does not add the amount back twice. Reversal corrects
the recorded payment; it does not send a refund.

If a payment or invoice changes while you are saving an edit or reversal, the action may report a conflict. Refresh
and review the latest balance before trying again. Changes that would leave inconsistent balances are rejected.

## Income by Unit

Income is grouped by unit by default. Each group is labeled with the unit and property, followed by the total invoice
amount, amount paid, and remaining balance, excluding voided invoices. Select a unit row to expand its finalized lease history, including all lease tenants and invoice details. Select an invoice row to open that invoice's details.

Expanded rows show the invoice ID, due date, status, amount, balance, and payment details when payments have been
recorded.

Select the **Grouped By Unit** toggle to switch to an ungrouped rent-roll view. This lists saved invoices with their property, unit, tenants, due date, status, recorded payments, and balance.

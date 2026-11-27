---
title: Lease Details
slug: /lease-details
---
Open a lease detail page by selecting a lease from the **Leases** dashboard.

On mobile, header actions collapse into the **Actions** menu. On larger screens, primary actions appear beside the menu.

## Summary

The summary header shows the property, unit, lease term, and current lease status. A lease without an end date is
shown as **Month-to-Month**.

Scheduled leases activate on their start date in the organization's timezone. Fixed-term leases end after their
last day, unless they continue month-to-month. These changes update occupancy without generating invoices.
The worker checks PostgreSQL at startup and periodically, so leases still transition after a missed queue job or
worker downtime.

Expand **Lease activity** at the bottom of the page to view its log. It is collapsed by default.
It lists finalization, successful activations and expirations,
plus transition failures that need attention. **Lease started** shows the effective lease start date, including
leases that become active immediately when created or finalized. The event timestamp records when activation
was logged; it can differ from the start date. Existing active or notice leases without an activation log
show their start date and **Log timestamp unavailable**. If
activation or expiration failed, a user with **Leases → Edit** can choose **Retry activation** or **Retry expiration**
from **Actions** once the start date has arrived or the end date has passed, respectively. Reconciliation also keeps
retrying eligible leases automatically.

The metric cards show the monthly rent and the rent due day. If no rent due date is available, Parcelis shows
**Not set**.

## Lease Information

The Lease Information card includes:

- Property
- Unit
- Lease start and end dates
- Monthly rent
- Rent due date

Select the property or unit to open its corresponding detail page.

## Associated Tenants

The Associated Tenants card lists the current residents of the lease. Select a tenant to open their lease record in a drawer.

For a shared lease, each tenant card also lists the other **Co-tenants**. Select a co-tenant's name to open
their tenant profile. The tenant lease record drawer shows everyone assigned to the selected lease,
including the tenant whose record is open. These lists reflect the lease's saved tenant assignments.
Single-tenant cards do not show a co-tenant list.

## Amend a Finalized Lease

Choose **Edit Lease** to revise rent, the due day, or the end date of a fixed term. Choose
**Actions → Edit Tenants** to update the roster. The security deposit total stays fixed.

1. Choose the lease start date or the first day of a future billing month in the organization's time zone.
2. Enter the changes and a reason, then select **Preview invoices**. Review the invoices to add, update, or remove.
3. Select **Apply amendment**. If the preview expires or an invoice changes, review a fresh preview before applying.

![Lease amendment invoice preview with an updated rent amount and due date](/img/lease-amendment-preview.png)

The current rent, end date, and residents remain visible until the amendment takes effect. **Lease activity**
records the reason, effective date, and revised terms. Returning residents keep their earlier occupancy history.

For a month-to-month lease, the preview covers 12 billing months starting on the effective date.
Invoices for periods that start before the effective date and invoices with issuance, payment history, manual
edits, or notes are protected. Invoices already due are also protected. Upgrading protects earlier rent invoices
because prior versions did not track PDF downloads. New rent invoice PDFs are marked issued when downloaded.

Amendments are available on scheduled, active, and notice leases. Preview requires **Leases → View and Edit**
and **Invoices → View**. Apply also requires **Invoices → Edit**, plus **Create** for added invoices or
**Delete** for removed invoices. Changing the roster, billing responsibility, or tenant shares requires
**Tenants → View**. Changing rent on an individually billed lease also requires updating its tenant shares.

## Archive or Delete a Lease

Open **Actions → Archive Lease** and confirm to hide a lease from the default lease directory. Archiving preserves its status, tenant assignments, and invoices; it does not terminate the lease or change occupancy. Use the directory's **Archive Status** filter to find archived leases, then **Actions → Unarchive Lease** to restore one.

Use **Actions → Delete Lease** only for a draft without invoices. Deletion requires confirmation and permanently removes the draft and its tenant assignments. Existing tenant records remain available.

Opening a lease detail URL requires **Leases → View**, independently of property viewing permission. If loading your permissions fails, select **Retry** to try again.

Lease actions use lease permissions independently of property permissions. Viewing or editing properties does not grant access to lease records or lifecycle actions.

---
title: Installation Identity
slug: /installation-identity
---

Parcelis creates a persistent installation ID when the first account is successfully created. This identifies the self-hosted installation independently of its users, organizations, and licensing.

## When the ID is created

Account registration saves the installation ID in the same database transaction as the new account, its organization, and the verification-email outbox entry. If registration fails, the identity is rolled back with the account. The ID is created when the account is registered, before email verification.

For installations configured with the administrator seed command, the administrator-account transaction initializes the same installation record. Rerunning the seed command preserves an existing ID.

An existing deployment without an installation record receives one on its next successful account registration or administrator seed run. Starting license activation also creates the ID if it is missing. Starting the API, signing in, and verifying an email do not create or replace the ID.

## Find the installation ID

Organization owners and administrators can open **Settings → Organization → Installation** to see the app version and installation ID. Select **Copy installation ID** to share it with support. The same ID appears in each organization on the installation.

If the page says an ID hasn’t been created yet, it will appear when one of the actions above creates it.

## Persistence

The UUID and its creation timestamp are stored in the installation database. Later account registrations and concurrent setup attempts reuse the same record. Restarting the app or restoring that installation's database backup preserves its ID.

The ID belongs to the database-backed installation, rather than a particular user, organization, container, or physical server. Copying a database also copies the ID. This change does not provide a reset or regeneration action for creating a separate installation from a database clone.

## Relationship to licensing

Creating an installation ID requires no Parcelis Portal login, activation code, licensing environment variables, or connection to Accounts. It does not enroll or activate the installation.

The installation ID is an identifier, not an authentication secret or a license key. Public account-registration responses do not include it.

Unlinking keeps the local installation ID and the portal’s registration history. The next activation uses a new registration and credential.

Set `NEXTAUTH_URL` on the self-hosted app to the address where you open Parcelis. The activation form previews this address. Parcelis shares it with the Portal on activation and refresh. Parcelis reports the version in the web app’s package manifest on activation and refresh.

## Rollout

Apply the database migrations before creating accounts, running the administrator seed command, or activating a license. Include the installation and license records in normal database backups. License activation requires outbound HTTPS access to Parcelis Portal and its public signing-key endpoint. Installations that stay unlinked need no Portal connectivity.

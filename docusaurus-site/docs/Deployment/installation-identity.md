---
title: Installation Identity
slug: /installation-identity
---

Parcelis creates a persistent installation ID when the first account is successfully created. This identifies the self-hosted installation independently of its users, organizations, and licensing.

## When the ID is created

Account registration saves the installation ID in the same database transaction as the new account, its organization, and the verification-email outbox entry. If registration fails, the identity is rolled back with the account. The ID is created when the account is registered, before email verification.

For installations configured with the administrator seed command, the administrator-account transaction initializes the same installation record. Rerunning the seed command preserves an existing ID.

An existing deployment without an installation record receives one on its next successful account registration or administrator seed run. Starting the API, signing in, and verifying an email do not create or replace the ID.

## Persistence

The UUID and its creation timestamp are stored in the installation database. Later account registrations and concurrent setup attempts reuse the same record. Restarting the app or restoring that installation's database backup preserves its ID.

The ID belongs to the database-backed installation, rather than a particular user, organization, container, or physical server. Copying a database also copies the ID. This change does not provide a reset or regeneration action for creating a separate installation from a database clone.

## Relationship to licensing

Creating an installation ID requires no Parcelis Accounts login, activation code, licensing environment variables, or connection to Accounts. It does not enroll or activate the installation.

The installation ID is an identifier, not an authentication secret or a license key. This backend change stores it for later use; it does not add a Settings screen or return it in public account-registration responses.

## Rollout

Apply the database migration before creating accounts or running the administrator seed command. Include the installation record in normal database backups. No additional runtime configuration is required.

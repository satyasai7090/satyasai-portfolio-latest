---
title: Upgrade notes
seo_title: "Nexus MFT 4.2.0: Upgrade Notes | Satya Sai Pasupuleti"
description: "How to prepare for, run and validate the Nexus MFT 4.2.0 upgrade."
---

# Upgrade notes

This section provides detailed guidance to help users and administrators prepare for, execute, and validate the Nexus MFT 4.2.0 upgrade. Following these notes will ensure a secure, smooth transition with minimal disruption.

## Pre-upgrade preparation

Before beginning the upgrade, complete these preparatory steps to ensure data integrity and a seamless process:

- Perform a full backup of the Nexus MFT database (SQL Server, PostgreSQL, or Oracle).
- Ensure the host machine has Java Runtime Environment (JRE) 17 or higher installed.
- Verify that your license key supports version 4.x features.
- Audit existing PGP keys; any keys using the deprecated SHA-1 hashing should be updated.
- Verify that server environments meet the minimum system requirements for version 4.2.0, including OS version, browser support, and available disk space.

## Upgrade process

The upgrade process introduces a brief service interruption and activates new security features. Follow these steps to upgrade to Nexus MFT version 4.2.0:

1. Log in to the Nexus MFT admin portal and navigate to **System Administration** > **Updates**.
2. Click **Check for Updates** and confirm that version 4.2.0 is available.
3. Stop the Nexus MFT service and all associated Edge Agents.
4. Run `Nexus_MFT_4.2.0_Setup.exe` (Windows) or `nexus-mft-upgrade.sh` (Linux).
5. The installer automatically detects the existing configuration and prompts for a database schema update.
6. Once the schema update is complete, start the service.
7. Access the admin console to verify the version in **System** > **Information**.
8. Notify all users that the system is available, and they may proceed with login and any required MFA setup.

## Post-upgrade tasks

After completing the upgrade to Nexus MFT 4.2.0, administrators should perform the following tasks to ensure the system's stability and integrity:

- Clear the browser cache to ensure the new React-based UI loads correctly.
- Test connectivity for at least one SFTP and one AS2 partner to validate protocol listeners.
- If using OAuth2, register the new redirect URI in your identity provider portal.

## Troubleshooting and support

If any issues are encountered during or after the upgrade, administrators should take the following actions:

| Issue | Action |
|---|---|
| The service fails to start | Check `logs/wrapper.log` for Java version conflicts. |
| SQL connection errors | Verify that the service account has `ALTER` permissions for the schema update phase. |
| Urgent or unresolved issues | Contact support@nexusmft.com for direct help. |

Refer to the in-app support resources and knowledge base articles for additional troubleshooting guidance and best practices.

These upgrade instructions aim to ensure a controlled, positive experience as your organization transitions to Nexus MFT 4.2.0. For further help, see [Known issues and support](known-issues.md).

[Next: Known issues and support →](known-issues.md)

---
title: Upgrade notes
seo_title: "CloudSuite CRM 3.12.0: Upgrade Notes | Satya Sai Pasupuleti"
description: "How to prepare for, run and validate the CloudSuite CRM 3.12.0 upgrade."
---

# Upgrade notes

This section provides detailed guidance to help users and administrators prepare for, execute, and validate the CloudSuite CRM 3.12.0 upgrade. Following these notes will ensure a secure, smooth transition with minimal disruption.

## Pre-upgrade preparation

Before beginning the upgrade, complete these preparatory steps to ensure data integrity and a seamless process:

- Back up all custom data, generated reports, and connected third-party integrations, in accordance with your organization's IT policies.
- Review these release notes and change logs to familiarize yourself with new features, deprecated components, and resolved issues.
- Notify all users of the planned upgrade window and estimated downtime.
- Ensure all users have their latest contact information (especially for MFA).
- Verify that server environments meet the minimum system requirements for version 3.12.0, including OS version, browser support, and available disk space.

## Upgrade process

The upgrade process introduces a brief service interruption and activates new security features. Follow these steps to upgrade to CloudSuite CRM 3.12.0:

1. Log in to the CloudSuite CRM admin portal and navigate to **System Administration** > **Updates**.
2. Click **Check for Updates** and confirm that version 3.12.0 is available.
3. In the **Updates** panel, select **Upgrade to 3.12.0**.
4. Review and accept the End User License Agreement (EULA) and release notes summary when prompted.
5. Click **Proceed with Upgrade** to initiate the update.
6. Monitor the progress bar and system logs for any error messages.
7. After the upgrade completes, the system will automatically restart all CRM services.
8. Log back into the admin portal and verify that version 3.12.0 is active.
9. Notify all users that the system is available, and they may proceed with login and any required MFA setup.

!!! warning "Do not close the admin portal"
    Do not close the admin portal while the upgrade is in progress. Expected duration: 10–30 minutes.

## Post-upgrade tasks

After completing the upgrade to CloudSuite CRM 3.12.0, administrators should perform the following tasks to ensure the system's stability and integrity:

- Review user role assignments and permissions, as new default groups and updated access controls may affect existing configurations.
- Validate all integration points and API connections; update or regenerate API keys if API rate limits or third-party access require it.
- Confirm users are accessing CloudSuite CRM through supported browsers (Microsoft Edge, Google Chrome, or Mozilla Firefox). Internet Explorer 11 is no longer supported.
- Check that custom dashboards, notification settings, workflows, scheduled jobs, and automated backups are functioning as expected.
- Communicate the successful completion of the upgrade, highlighting any relevant updates or actions, to all users.

## Troubleshooting and support

If any issues are encountered during or after the upgrade, administrators should take the following actions:

| Issue | Action |
|---|---|
| Login or connectivity problems | Clear the browser cache and attempt to log in again. |
| API integrations or webhooks fail | Re-register the webhooks and generate new API keys as required. |
| Discrepancies in data migration, dashboard layouts, or account access | Report them through the CloudSuite CRM support portal for prioritized assistance. |
| Urgent or unresolved issues | Contact support@cloudsuitecrm.com for direct help. |

Refer to the in-app support resources and knowledge base articles for additional troubleshooting guidance and best practices.

These upgrade instructions aim to ensure a controlled, positive experience as your organization transitions to CloudSuite CRM 3.12.0. For further help, see [Known issues and support](known-issues.md).

[Next: Known issues and support →](known-issues.md)

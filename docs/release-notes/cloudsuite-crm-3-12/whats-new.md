---
title: What's new
seo_title: "CloudSuite CRM 3.12.0: What's New | Satya Sai Pasupuleti"
description: "Added features, changed features, fixed bugs, security updates and deprecations in CloudSuite CRM 3.12.0."
---

# What's new in CloudSuite CRM 3.12.0

This section details the key new features, enhancements, updates, security changes, and deprecations introduced in CloudSuite CRM 3.12.0. All items are grouped for clear traceability and fast reference.

## Added features

The following features have been newly introduced in this release to improve productivity, security, and user experience:

| Feature | Description |
|---|---|
| AI-powered lead scoring | Machine learning models automatically evaluate and rank leads, helping sales teams focus on the most promising opportunities. |
| Customizable dashboard widgets | Users can personalize their dashboards using drag-and-drop widgets, saving preferred layouts for fast, individualized access. |
| In-app guided walkthroughs | Interactive onboarding and tutorial flows accelerate learning of new features and improve user adoption. |
| Multi-factor authentication (MFA) | Support for TOTP (time-based one-time password) and SMS code verification to enhance account security. |

## Changed features

The following existing functionalities have been enhanced or modified in this release:

| Feature | Change |
|---|---|
| Contact import workflow | Updated with real-time progress indicators, improved error messaging, and enhanced mapping for custom fields. |
| Email template editor | Modernized interface featuring rich text editing, snippet insertion, real-time preview, and better accessibility. |
| API rate limits | Adjusted thresholds to improve system performance and reliability. Refer to the developer documentation for updated values. |

## Fixed bugs

The following issues identified as bugs in previous versions have been resolved:

- Calendar synchronization for recurring events now works reliably in all supported time zones.
- Export of large custom reports (over 10,000 rows) completes successfully without intermittent errors.
- Notification badges in the mobile app now clear correctly after messages are viewed.
- Role-based access for team dashboards displays the correct content per assigned permissions.

## Security updates

- Patched a cross-site scripting (XSS) vulnerability in user profile image uploads.
- Session timeouts have been shortened to reduce unauthorized session risks.
- All inputs to the feedback form are now thoroughly validated to protect against injection attacks.

## Deprecated features

!!! warning "Legacy email reports"
    The classic scheduled email reports feature is being phased out and will be removed in version 4.0. All users should migrate to the Automated Insights feature by September 2025.

[Next: Upgrade notes →](upgrade.md)

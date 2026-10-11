---
title: What's new
seo_title: "Nexus MFT 4.2.0: What's New | Satya Sai Pasupuleti"
description: "Added features, changed features, fixed bugs, security updates and deprecations in Nexus MFT 4.2.0."
---

# What's new in Nexus MFT 4.2.0

This section details the key technical enhancements and security hardening introduced in version 4.2.0.

## Added features

The following features have been newly introduced in this release to improve productivity, security, and user experience:

| Feature | Description |
|---|---|
| OAuth2/OIDC support | Integration with external identity providers (IdP) such as Okta, Azure AD, and PingFederate for single sign-on (SSO). |
| S3-compatible storage connectors | Ability to mount any S3-compliant object storage as a virtual folder with client-side encryption. |
| Automated PGP key rotation | Configurable policies to automatically rotate PGP keys for trading partners to maintain security hygiene. |
| Event-driven webhooks | Real-time notifications for transfer success, failure, or file-integrity check events sent to external SIEM or Slack/Teams channels. |

## Changed features

The following existing functionalities have been enhanced or modified in this release:

| Feature | Change |
|---|---|
| Advanced scheduler logic | Enhanced "Holiday Awareness" and "Retry-on-Network-Failure" logic for complex global transfer windows. |
| SFTP engine performance | Upgraded Java SSH library to improve performance by 25% during high-concurrency SFTP transfers. |
| Web Client UI | Transitioned from legacy frameworks to a modern React-based responsive dashboard for improved administrator UX. |

## Fixed bugs

The following issues identified as bugs in previous versions have been resolved:

- Resolved a bug where SFTP transfers would fail on specific Linux-to-Windows cross-platform mounts due to filename casing.
- Patched a heap memory leak in the AS2 MDN listener that occurred after 48 hours of continuous high-volume uptime.
- Fixed an issue where the "Live Monitor" dashboard stopped updating after a session timeout without prompting for re-authentication.

## Security updates

- Added an option to disable legacy TLS 1.1/1.2 protocols to enforce modern cipher suites.
- Removed support for weak MAC algorithms (HMAC-MD5, HMAC-SHA1) to align with current NIST guidelines.
- Added brute-force protection to the HTTPS web client and SFTP listener.

## Deprecated features

!!! warning "Deprecations in this release"
    - **Legacy API v1:** Version 1 of the REST API is officially deprecated and will be removed in version 5.0.
    - **IE11 support:** The Nexus MFT Web Client no longer supports Internet Explorer 11.

[Next: Upgrade notes →](upgrade.md)

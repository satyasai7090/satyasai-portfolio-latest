---
title: Troubleshoot connection issues
seo_title: "Nexus MFT Knowledge Base Sample | Satya Sai Pasupuleti"
description: "Symptom-based troubleshooting articles for a managed file transfer platform: connection failures, transfer performance and authentication errors. Writing sample by Satya Sai Pasupuleti."
---

!!! abstract "About this sample"
    - **What this is** A troubleshooting knowledge base for Nexus MFT, a fictional managed file transfer platform. Three articles cover connection issues, transfer performance and authentication errors.
    - **Audience** Administrators, integration engineers and support engineers.
    - **Tools used** Markdown, MkDocs Material, Microsoft Writing Style Guide.
    - **What it demonstrates** Troubleshooting organized by symptom rather than error code. Every entry gives the cause and numbered resolution steps, with commands where they help.
    - **Note** Nexus MFT is a fictional product created for this sample. It shares its product world with the [Nexus MFT API documentation](../../api-docs/nexus-mft/index.md).

# Troubleshoot connection issues

Use this article to diagnose and resolve connection failures between Nexus MFT and your source or destination endpoints.

!!! note "Before you start"
    Make sure you have access to the Admin Console and the transfer error details. To find the error details, go to **Transfers** and select the failed transfer.

## Transfer fails with a "Connection refused" error

**Cause:** The destination server is unreachable. The server might be down, or a firewall rule is blocking the connection on the required port.

**Resolution:**

1. Verify that the destination server is running and accepting connections.
2. Check that your firewall allows outbound traffic on the required port (SFTP: 22, FTPS: 990, HTTPS: 443).
3. Test connectivity from the Nexus MFT server.
4. If the destination uses IP allowlisting, confirm that the Nexus MFT egress IP addresses are on the allowlist.

```bash
# Test connectivity from the command line
nc -zv destination-server.com 22

# Expected output if successful:
# Connection to destination-server.com 22 port [tcp/ssh] succeeded!
```

## Transfer hangs at "Connecting..." and times out

**Cause:** A network route between the Nexus MFT server and the destination is dropping packets. This commonly happens when a firewall silently drops traffic instead of rejecting it.

**Resolution:**

1. Check the network route between the source and destination using `traceroute`.
2. Verify that no intermediate firewalls or proxy servers are silently dropping connections.
3. If the destination has high latency, increase the connection timeout in the endpoint configuration.
4. Ask your network administrator to verify that the route is stable.

## SFTP connection fails with "Host key verification failed"

**Cause:** The destination server's SSH host key doesn't match the key stored in the Nexus MFT `known_hosts` file. This can happen when the destination server is rebuilt or its SSH keys are rotated.

**Resolution:**

1. Go to **Settings** > **Endpoints** in the Admin Console.
2. Select the affected endpoint, and then select **Edit**.
3. Under **Host Key Verification**, select **Update Host Key**.
4. Verify that the new host key fingerprint matches the value from your server administrator.
5. Save the endpoint configuration and retry the transfer.

[Next: Troubleshoot transfer performance →](performance.md)

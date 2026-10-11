---
title: Troubleshoot authentication errors
seo_title: "Nexus MFT: Troubleshoot Authentication Errors | Satya Sai Pasupuleti"
description: "Resolve 401 and 403 API errors and SFTP authentication failures in Nexus MFT."
---

# Troubleshoot authentication errors

Use this article to resolve authentication and authorization errors when you connect to the Nexus MFT API or configure endpoint credentials.

!!! warning "Security reminder"
    Never share API keys or credentials in support tickets, chat messages or emails. If you suspect that a key is compromised, revoke it immediately from the Admin Console.

## API returns 401 Unauthorized on every request

**Cause:** Your API key is missing from the request, incorrectly formatted or expired.

**Resolution:**

1. Verify that your request includes the `Authorization` header in the format `Bearer YOUR_API_KEY`.
2. Check that the API key has no extra spaces or line breaks.
3. Go to **Settings** > **API Keys** in the Admin Console and verify that the key hasn't expired.
4. If the key has expired, generate a new key and update your integration.

```bash
# Correct format
curl -H "Authorization: Bearer sk_live_abc123def456" ...

# Common mistakes:
# - Missing "Bearer" prefix
# - Extra space: "Bearer  sk_live_abc123def456"
# - Using the key ID instead of the key value
```

## API returns 403 Forbidden for specific operations

**Cause:** Your API key doesn't have the permission that the operation requires.

**Resolution:**

1. Check which permission the operation requires in the [API reference](../../api-docs/nexus-mft/authentication.md#api-key-permissions).
2. Go to **Settings** > **API Keys** and select the key you're using.
3. Verify that the key has the required permission scope.
4. If the permission is missing, generate a new key with the correct permissions. You can't change a key's permissions after you create it.

## SFTP sign-in fails with "Authentication failed"

**Cause:** The credentials stored in the endpoint configuration are incorrect, or the user account on the destination server is disabled or locked.

**Resolution:**

1. Go to **Settings** > **Endpoints** and select the affected endpoint.
2. Verify that the username and password, or the SSH key, are correct.
3. Test the credentials manually by connecting to the SFTP server from a terminal.
4. If you use key-based authentication, verify that the public key is in the `authorized_keys` file on the destination server.
5. Ask the server administrator whether the account is active and unlocked.

```bash
# Test SFTP credentials manually with a key
sftp -i /path/to/private_key user@destination-server.com

# Or with password authentication
sftp user@destination-server.com
```

## Still need help?

If the issue continues after you follow these steps, collect the following information before you contact support:

- The full error message, with any credentials or API keys removed
- The transfer ID or request ID from the API response
- The endpoint configuration name
- The time of the failed attempt, in UTC

[← Back to connection issues](index.md)

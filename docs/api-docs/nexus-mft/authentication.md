---
title: Authentication and security
seo_title: "Nexus MFT API Authentication | Satya Sai Pasupuleti"
description: "How to authenticate Nexus MFT API requests, generate, scope and rotate API keys, and restrict access by IP address."
---

# Authentication and security

All requests to the Nexus MFT API require authentication. The API uses Bearer token authentication to verify your identity and authorize access to resources.

## Authenticate your requests

Include your API key in the `Authorization` header of every request.

```text
Authorization: Bearer YOUR_API_KEY
```

## Generate an API key

To generate a new API key:

1. Sign in to the Nexus MFT Admin Console.
2. Go to **Settings** > **API Keys**.
3. Select **Create API Key**.
4. Enter a descriptive name for the key, for example "Production - Transfer Service".
5. Select the permissions you want to assign to the key.
6. Select **Generate**.

!!! warning "Important"
    Copy and store your API key immediately after you generate it. For security reasons, the full key is shown only once. If you lose it, you must generate a new key.

## API key permissions

You can scope each API key to specific permissions. Assign only the permissions that your integration requires.

| Permission | Scope | Description |
|---|---|---|
| `transfers:read` | Read | List and view transfer details. |
| `transfers:write` | Write | Create and cancel transfers. |
| `webhooks:manage` | Admin | Create, update and delete webhook subscriptions. |
| `endpoints:manage` | Admin | Configure source and destination endpoints. |
| `audit:read` | Read | View audit logs and transfer history. |

## Rotate your API keys

To maintain security, rotate your API keys regularly. When you rotate a key, the old key remains active for 24 hours so you have time to update your integrations.

To rotate an API key:

1. Go to **Settings** > **API Keys** in the Admin Console.
2. Find the key you want to rotate and select **Rotate**.
3. Copy the new key and update your integration.
4. Verify that your integration works with the new key.

The old key is revoked automatically after 24 hours.

## Security best practices

- Never expose API keys in client-side code or public repositories.
- Use environment variables or a secrets manager to store your keys.
- Assign the minimum permissions required for each integration.
- Monitor the audit log for unexpected API activity.
- Rotate keys every 90 days, or immediately if you suspect a compromise.

## IP allowlisting

For additional security, you can restrict API access to specific IP addresses. When you turn on IP allowlisting, the API rejects requests from IP addresses that aren't on your list.

```json
{
  "allowed_ips": [
    "203.0.113.10",
    "198.51.100.0/24"
  ],
  "enforce": true
}
```

To configure IP allowlisting, go to **Settings** > **Security** > **IP Allowlist** in the Admin Console.

[Next: Webhooks and events →](webhooks.md)

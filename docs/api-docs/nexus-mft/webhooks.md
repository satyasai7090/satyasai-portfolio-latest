---
title: Webhooks and events
seo_title: "Nexus MFT API Webhooks | Satya Sai Pasupuleti"
description: "How to register Nexus MFT webhooks, the events they deliver, payload format, signature verification and retry behavior."
---

# Webhooks and events

Use webhooks to receive real-time notifications when events occur in your Nexus MFT account. Instead of polling the API for status updates, you can configure the system to send HTTP POST requests to your endpoint when a transfer completes, fails or needs attention.

## How webhooks work

1. You register a webhook endpoint URL and select the events you want to subscribe to.
2. When a subscribed event occurs, the system sends an HTTP POST request to your endpoint.
3. Your endpoint processes the payload and returns a `200` status code to acknowledge receipt.
4. If your endpoint doesn't respond within 10 seconds or returns a non-2xx status, the system retries up to 3 times with exponential backoff.

## Register a webhook

To register a new webhook, send a POST request to the `/webhooks` endpoint.

```bash
curl -X POST "https://api.nexusmft.io/v1/webhooks" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-app.com/webhooks/nexus",
    "events": [
      "transfer.completed",
      "transfer.failed"
    ],
    "secret": "whsec_your_signing_secret"
  }'
```

## Supported events

| Event | Trigger |
|---|---|
| `transfer.created` | A new transfer job is created. |
| `transfer.in_progress` | A transfer begins processing. |
| `transfer.completed` | A transfer finishes successfully. |
| `transfer.failed` | A transfer fails after all retry attempts. |
| `transfer.cancelled` | A user or API call cancels a transfer. |
| `endpoint.connectivity_lost` | A configured endpoint becomes unreachable. |
| `key.expiring_soon` | An API key will expire within 7 days. |

## Webhook payload

Each webhook delivery includes a JSON payload with the event type, timestamp and the relevant resource data.

```json
{
  "id": "evt_a1b2c3d4",
  "type": "transfer.completed",
  "created_at": "2025-12-15T09:30:12Z",
  "data": {
    "transfer_id": "txr_8a3b1c2d",
    "file_name": "report_Q4_2025.csv",
    "size_bytes": 2048576,
    "status": "completed",
    "source": "sftp://uploads.acme.com/outbox",
    "destination": "s3://acme-archive/reports/",
    "duration_ms": 12000,
    "checksum_sha256": "a3f2c1...e8d9b4"
  }
}
```

## Verify webhook signatures

Every webhook request includes an `X-Nexus-Signature` header. Use this header to verify that the request came from Nexus MFT and wasn't tampered with.

To verify the signature:

1. Compute an HMAC-SHA256 hash of the raw request body, using your webhook secret as the key.
2. Compare the computed hash with the value in the `X-Nexus-Signature` header.
3. If the values match, the request is authentic. If they don't match, reject the request.

!!! danger "Security"
    Always verify webhook signatures before you process the payload. This prevents attackers from sending fraudulent webhook events to your endpoint.

## Retry behavior

If your endpoint doesn't respond with a 2xx status code within 10 seconds, the system retries the delivery. The retry schedule uses exponential backoff:

- First retry: 1 minute after the initial attempt
- Second retry: 5 minutes after the first retry
- Third retry: 30 minutes after the second retry

After 3 failed attempts, the event is marked as failed. You can view failed deliveries and retry them manually from the Admin Console under **Webhooks** > **Failed Deliveries**.

[← Back to the API reference](index.md)

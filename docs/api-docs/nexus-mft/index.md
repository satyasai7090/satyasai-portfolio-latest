---
title: Nexus MFT API reference
seo_title: "Nexus MFT REST API Documentation Sample | Satya Sai Pasupuleti"
description: "REST API documentation set for a managed file transfer platform: endpoints, authentication, API key permissions, webhooks and error handling. Writing sample by Satya Sai Pasupuleti."
---

!!! abstract "About this sample"
    - **What this is** A three-part REST API documentation set for Nexus MFT, a fictional managed file transfer platform. It covers the endpoint reference, authentication and security, and webhooks.
    - **Audience** Developers and integration engineers who automate file transfers.
    - **Tools used** Markdown, MkDocs Material, Microsoft Writing Style Guide.
    - **What it demonstrates** Task-based API documentation: every endpoint has parameters, a request and a response, and security steps are written as procedures a developer can follow.
    - **Note** Nexus MFT is a fictional product created for this sample. The structure reflects the kind of managed file transfer documentation I work on professionally.

# API reference

Use the Nexus MFT REST API to manage file transfers programmatically. You can create, monitor and cancel transfers across your infrastructure.

**Base URL**

```text
https://api.nexusmft.io/v1
```

## Before you begin

To use the API, you need an API key with the appropriate permissions. For instructions on how to generate and manage API keys, see [Authentication and security](authentication.md).

## Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/transfers` | [List all file transfers](#list-all-file-transfers) |
| `POST` | `/transfers` | [Create a file transfer](#create-a-file-transfer) |
| `GET` | `/transfers/{transfer_id}` | [Get transfer details](#get-transfer-details) |
| `DELETE` | `/transfers/{transfer_id}` | [Cancel a transfer](#cancel-a-transfer) |

### List all file transfers

<span class="method get">GET</span> `/transfers`

Returns a paginated list of file transfers for your account. You can filter results by status, date range and destination.

**Parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `status` | string | Optional | Filter by transfer status. Accepted values: `pending`, `in_progress`, `completed`, `failed`. |
| `from_date` | string | Optional | ISO 8601 date. Returns transfers created on or after this date. |
| `to_date` | string | Optional | ISO 8601 date. Returns transfers created on or before this date. |
| `limit` | integer | Optional | Number of results per page. Default: 25. Maximum: 100. |
| `offset` | integer | Optional | Number of results to skip. Use this for pagination. |

**Request example**

```bash
curl -X GET "https://api.nexusmft.io/v1/transfers?status=completed&limit=10" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Accept: application/json"
```

**Response** `200`

```json
{
  "data": [
    {
      "id": "txr_8a3b1c2d",
      "file_name": "report_Q4_2025.csv",
      "size_bytes": 2048576,
      "status": "completed",
      "source": "sftp://uploads.acme.com/outbox",
      "destination": "s3://acme-archive/reports/",
      "created_at": "2025-12-15T09:30:00Z",
      "completed_at": "2025-12-15T09:30:12Z"
    }
  ],
  "pagination": {
    "total": 142,
    "limit": 10,
    "offset": 0,
    "has_more": true
  }
}
```

### Create a file transfer

<span class="method post">POST</span> `/transfers`

Creates a new file transfer job. The system queues the transfer immediately and processes it based on priority and server availability.

**Parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `source_uri` | string | Required | URI of the source file. Supported protocols: `sftp://`, `ftps://`, `s3://`, `azure://`. |
| `destination_uri` | string | Required | URI of the destination. You must pre-configure the endpoint in the Admin Console. |
| `priority` | string | Optional | Transfer priority. Accepted values: `low`, `normal`, `high`. Default: `normal`. |
| `notify_on_complete` | boolean | Optional | Set to `true` to receive a webhook notification when the transfer finishes. Default: `false`. |
| `metadata` | object | Optional | Custom key-value pairs. Maximum: 10 keys, 256 characters per value. |

**Request example**

```bash
curl -X POST "https://api.nexusmft.io/v1/transfers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "source_uri": "sftp://uploads.acme.com/outbox/report.csv",
    "destination_uri": "s3://acme-archive/reports/",
    "priority": "high",
    "notify_on_complete": true,
    "metadata": {
      "department": "finance",
      "quarter": "Q4-2025"
    }
  }'
```

**Response** `201`

```json
{
  "id": "txr_9f4e2d1a",
  "status": "pending",
  "source_uri": "sftp://uploads.acme.com/outbox/report.csv",
  "destination_uri": "s3://acme-archive/reports/",
  "priority": "high",
  "created_at": "2025-12-15T14:22:00Z",
  "estimated_start": "2025-12-15T14:22:05Z"
}
```

### Get transfer details

<span class="method get">GET</span> `/transfers/{transfer_id}`

Returns detailed information about a specific file transfer, including progress, transfer speed and error details if the transfer failed.

**Parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `transfer_id` | string | Required | The unique identifier of the transfer. This is a path parameter. |

**Request example**

```bash
curl -X GET "https://api.nexusmft.io/v1/transfers/txr_8a3b1c2d" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Response** `200`

```json
{
  "id": "txr_8a3b1c2d",
  "file_name": "report_Q4_2025.csv",
  "size_bytes": 2048576,
  "transferred_bytes": 2048576,
  "progress_pct": 100,
  "status": "completed",
  "speed_bps": 170714,
  "source": "sftp://uploads.acme.com/outbox",
  "destination": "s3://acme-archive/reports/",
  "checksum_sha256": "a3f2c1...e8d9b4",
  "created_at": "2025-12-15T09:30:00Z",
  "completed_at": "2025-12-15T09:30:12Z",
  "retry_count": 0,
  "error": null
}
```

### Cancel a transfer

<span class="method delete">DELETE</span> `/transfers/{transfer_id}`

Cancels a transfer that has a status of `pending` or `queued`. You can't cancel transfers that are already in progress.

**Parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `transfer_id` | string | Required | The unique identifier of the transfer to cancel. This is a path parameter. |

**Request example**

```bash
curl -X DELETE "https://api.nexusmft.io/v1/transfers/txr_9f4e2d1a" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Response** `200`

```json
{
  "id": "txr_9f4e2d1a",
  "status": "cancelled",
  "cancelled_at": "2025-12-15T14:23:00Z"
}
```

## Error codes

When a request fails, the API returns an HTTP status code and a JSON error object. The following table lists the standard error codes.

| Code | Status | Description |
|---|---|---|
| `400` | Bad Request | The request body is missing required fields or contains invalid values. |
| `401` | Unauthorized | Your API key is missing, invalid or expired. |
| `403` | Forbidden | Your API key doesn't have permission for this operation. |
| `404` | Not Found | The specified resource doesn't exist. |
| `409` | Conflict | The transfer can't be modified in its current state. |
| `429` | Rate Limited | You've exceeded the request limit. Wait for the time specified in the `Retry-After` header. |
| `500` | Internal Server Error | An unexpected error occurred. If this persists, contact support. |

## Rate limits

The API enforces rate limits to ensure fair usage. You can make up to 100 requests per minute per API key. If you exceed this limit, the API returns a `429` status code with a `Retry-After` header that indicates how long to wait before you retry.

!!! note "Rate limit headers"
    Every response includes the following headers:

    - `X-RateLimit-Limit`: maximum requests per minute
    - `X-RateLimit-Remaining`: requests remaining in the current window
    - `X-RateLimit-Reset`: Unix timestamp when the limit resets

[Next: Authentication and security →](authentication.md)

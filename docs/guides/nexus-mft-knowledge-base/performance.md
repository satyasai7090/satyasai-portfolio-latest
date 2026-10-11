---
title: Troubleshoot transfer performance
seo_title: "Nexus MFT: Troubleshoot Transfer Performance | Satya Sai Pasupuleti"
description: "Diagnose slow transfers, timeouts and file integrity failures in Nexus MFT."
---

# Troubleshoot transfer performance

Use this article to diagnose and resolve issues with transfer speed, timeouts and file integrity.

## Performance benchmarks

The following table shows expected transfer times under normal conditions. If your transfers are much slower than these values, use the troubleshooting steps in this article.

| File size | Expected duration at 100 Mbps | Expected duration at 1 Gbps |
|---|---|---|
| 10 MB | Under 2 seconds | Under 1 second |
| 100 MB | About 10 seconds | About 1 second |
| 1 GB | About 90 seconds | About 10 seconds |
| 10 GB | About 15 minutes | About 90 seconds |

## Transfers complete but are much slower than expected

**Cause:** The slowest link in the chain limits transfer speed. That link could be network bandwidth, server disk I/O or the Nexus MFT concurrency settings.

**Resolution:**

1. Check the transfer details to see the average speed (the `speed_bps` field in the API response).
2. Compare the transfer speed with your network bandwidth. If the transfer speed is below 50% of the available bandwidth, the bottleneck is likely on the endpoint side.
3. Go to **Settings** > **Performance** and increase **Max Concurrent Streams** (default: 4, maximum: 16).
4. For files larger than 1 GB, turn on chunked transfer mode to improve throughput.

## Transfers fail intermittently with "Timeout" errors

**Cause:** The transfer takes longer than the configured timeout. This commonly happens with large files on slow connections, or when the destination server is under heavy load.

**Resolution:**

1. Go to **Settings** > **Endpoints** and select the affected endpoint.
2. Increase the **Transfer Timeout** value. The default is 300 seconds (5 minutes).
3. For unreliable connections, turn on **Auto-Retry** with a maximum of 3 attempts.
4. If the issue continues, turn on checkpoint restart so that interrupted transfers resume where they stopped instead of starting over.

```bash
# Check the transfer timeout configuration through the API
curl -X GET "https://api.nexusmft.io/v1/endpoints/ep_abc123" \
  -H "Authorization: Bearer YOUR_API_KEY"

# Look for these fields in the response:
# "transfer_timeout_seconds": 300
# "auto_retry_enabled": false
# "max_retry_count": 0
```

## File integrity check fails after the transfer completes

**Cause:** The file was corrupted during transfer. An unstable network connection, or a misconfigured proxy that modifies the data stream, can cause this.

**Resolution:**

1. Verify that no proxy servers between Nexus MFT and the destination modify the data stream.
2. Turn on end-to-end checksum verification in the endpoint configuration. This computes a SHA-256 hash before and after the transfer.
3. If you use FTPS, make sure the data channel uses binary mode, not ASCII mode.
4. Retry the transfer. If the checksum fails again, contact support with the transfer ID.

[Next: Troubleshoot authentication errors →](authentication.md)

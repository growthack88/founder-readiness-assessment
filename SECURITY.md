# Security Policy

## Overview

The **Founder Readiness Assessment** is a fully client-side, static web application.

- ✅ No server-side code
- ✅ No database
- ✅ No user data collected or transmitted
- ✅ No cookies
- ✅ No authentication required
- ✅ All processing happens in the user's browser

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.0.x | ✅ Yes |

## Reporting a Vulnerability

If you discover a security issue (e.g., a way to inject malicious content), please:

1. **Do not** open a public GitHub Issue
2. Contact via [mahmoudomar.com](https://mahmoudomar.com)
3. Describe the issue, steps to reproduce, and potential impact

We will respond within 48 hours and coordinate a fix before any public disclosure.

## Dependencies

| Library | Version | Source | Notes |
|---------|---------|--------|-------|
| React | 18.2.0 | cdnjs.cloudflare.com | No known CVEs at release |
| ReactDOM | 18.2.0 | cdnjs.cloudflare.com | No known CVEs at release |
| Babel Standalone | 7.23.9 | cdnjs.cloudflare.com | Used only for JSX parsing |
| Google Fonts | — | fonts.googleapis.com | No executable code |

All external dependencies are loaded from trusted CDNs with fixed version pinning.

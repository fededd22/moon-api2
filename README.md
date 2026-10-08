# 🌙 Moon API — Server-Side Code Protection & Sandbox Engine

> Original source code **never leaves the server**. Users receive a lightweight client stub and a project API key only.

## 🚀 Overview

Moon API is a server-side execution and protection system for Python scripts and algorithms:
- **AES-256 / Fernet Encryption**: Source code is stored encrypted at rest with a master secret key.
- **Sandboxed Execution**: Runs functions and scripts in isolated processes with memory, CPU, file size, and execution timeouts.
- **API Key Access Control**: Per-project cryptographic API keys (`moon_...`) with TTL expiration, rate limiting, and instant revocation.
- **Client Stub Generator**: Generates clean, zero-logic client scripts (`client.py`) that forward function calls and arguments to the server.
- **Developer Dashboard**: Full interactive web interface with live sandbox execution, project management, API key issuance, client downloads, and audit logs.

## 🌐 API Endpoints

| Endpoint | Method | Authentication | Description |
|---|---|---|---|
| `/` | `GET` | None | System status and service watermark |
| `/api/health` | `GET` | None | Health check endpoint |
| `/api/run` | `POST` | `X-API-Key` | Execute function (`action="call"`) or script (`action="script"`) with stdin |
| `/api/functions` | `GET` | `X-API-Key` | List callable public functions in the protected project |
| `/api/info` | `GET` | `X-API-Key` | Project metadata and key expiration timestamp |
| `/api/client-stub` | `GET` | None | Generate or download client distribution stub |
| `/admin/projects` | `POST`/`GET` | `X-Admin-Key` | Create or list encrypted projects |
| `/admin/projects/:id`| `DELETE` | `X-Admin-Key` | Delete project and deactivate linked keys |
| `/admin/keys` | `POST`/`GET` | `X-Admin-Key` | Issue new project API key or list keys |
| `/admin/keys/:id` | `DELETE` | `X-Admin-Key` | Revoke API key |
| `/admin/logs` | `GET` | `X-Admin-Key` | Execution audit trail logs |

## 💻 Quickstart

### Run with Node.js
```bash
npm install
npm run dev
```

App runs on `http://0.0.0.0:3000`.

### Calling a Remote Function
```bash
curl -X POST http://0.0.0.0:3000/api/run \
  -H "X-API-Key: moon_demo_secret_key_12345" \
  -H "Content-Type: application/json" \
  -d '{"function": "fib", "args": [10]}'
```

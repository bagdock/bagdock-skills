# Bagdock

Bagdock is a platform for self-storage operators — apps and edges deploy to Cloudflare Workers for Platforms via the Bagdock API. Developers never need Cloudflare credentials.

## Authentication

API keys use a prefix convention:

| Prefix | Type | Usage |
|--------|------|-------|
| `bdok_sk_` | Secret | Server-side, full access |
| `bdok_pk_` | Publishable | Client-side, limited access |

Set via environment variable:

```bash
export BAGDOCK_API_KEY=bdok_sk_your_key_here
```

Or pass per-request:

```
Authorization: Bearer bdok_sk_your_key_here
```

The CLI also supports OAuth2 Device Authorization Grant for interactive login.

## API Base URL

```
https://api.bagdock.com/v1
```

## Key Endpoints

### Developer Apps

| Method | Path | Description |
|--------|------|-------------|
| GET | `/developer/apps` | List apps for authenticated operator |
| POST | `/developer/apps` | Create a new app |
| GET | `/developer/apps/:slug` | Get app details |
| PATCH | `/developer/apps/:slug` | Update app metadata |
| POST | `/developer/apps/:slug/deploy` | Upload script bundle to CF Workers |
| POST | `/developer/apps/:slug/submit` | Submit for marketplace review |
| GET | `/developer/apps/:slug/submissions` | List submission history |
| POST | `/developer/apps/:slug/submissions/:id/withdraw` | Withdraw pending submission |
| GET | `/developer/apps/:slug/env` | List env var keys |
| PUT | `/developer/apps/:slug/env` | Set an env var |
| DELETE | `/developer/apps/:slug/env/:key` | Remove an env var |

### API Keys

| Method | Path | Description |
|--------|------|-------------|
| POST | `/operator/api-keys` | Create a new API key |
| GET | `/operator/api-keys` | List API keys |
| GET | `/operator/api-keys/:id` | Get key detail |
| DELETE | `/operator/api-keys/:id` | Revoke a key |

### Logs

| Method | Path | Description |
|--------|------|-------------|
| GET | `/developer/apps/:slug/logs` | List recent log entries |

## Deployment Model

**Edges** are backend workers that connect external APIs, handle webhooks, and sync data between platforms.

**Apps** are UI extensions that add screens, panels, and drawers to the Bagdock operator dashboard.

Both deploy to Cloudflare Workers for Platforms via `POST /developer/apps/:slug/deploy` with a multipart form containing the compiled Worker bundle.

### URL Scheme

| Environment | Pattern | Description |
|-------------|---------|-------------|
| Production | `{slug}.bdok.dev` | Live, requires review for public |
| Staging | `{slug}.pre.bdok.dev` | Stable pre-production |
| Preview | `{slug}-{hash}.pre.bdok.dev` | Ephemeral, per-deploy |

## Marketplace Submission Lifecycle

1. Developer creates app: `POST /developer/apps` (status: `draft`)
2. Developer submits: `POST /developer/apps/:slug/submit` (status: `submitted`)
3. Bagdock reviews (status: `approved` or `rejected`)
4. Developer can withdraw before approval: `POST /developer/apps/:slug/submissions/:id/withdraw` (status: `draft`)

## Common Patterns

### Create and deploy an app

```bash
bagdock init --type edge --kind adapter --slug my-adapter
bagdock deploy --env staging
bagdock validate
bagdock submit
```

### Manage API keys

```bash
bagdock keys create --name "CI Deploy" --environment live
bagdock keys list
bagdock keys delete bdok_key_xxx
```

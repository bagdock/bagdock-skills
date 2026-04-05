# API Keys

Bagdock API keys are operator-scoped and used for programmatic access.

## Key Prefixes

Keys follow a Stripe-style prefix convention encoding type and environment:

| Prefix | Type | Environment | Description |
|--------|------|-------------|-------------|
| `sk_live_` | Secret | Production | Full API access, server-side only |
| `sk_test_{sandbox}_` | Secret | Sandbox | Full access, scoped to a sandbox |
| `pk_live_` | Publishable | Production | Limited client-side access |
| `pk_test_{sandbox}_` | Publishable | Sandbox | Limited access, sandbox-scoped |
| `rk_live_` | Restricted | Production | Scoped to specific permissions |
| `rk_test_` | Restricted | Sandbox | Scoped permissions, sandbox |
| `sk_personal_` | Personal | N/A | Per-user key |
| `ik_live_` | Internal | Production | System/AI detection only |
| `ik_test_` | Internal | Sandbox | System/AI detection only |

## Endpoints

### Create API Key

```
POST /v1/operator/api-keys
```

Body:
```json
{
  "name": "CI Deploy Key",
  "key_type": "secret",
  "key_category": "standard",
  "environment": "live",
  "scopes": ["apps:deploy", "apps:read"]
}
```

Response includes the raw key (shown once):
```json
{
  "data": {
    "id": "ak_xxx",
    "key": "sk_live_xxxxxxxxxxxxx",
    "key_prefix": "sk_live_xxxxxxxx"
  }
}
```

### List API Keys

```
GET /v1/operator/api-keys?environment=live&status=active
```

### Revoke API Key

```
DELETE /v1/operator/api-keys/:id
```

## Categories

| Category | Description |
|----------|-------------|
| `standard` | Default access |
| `restricted` | Limited to specific scopes |
| `personal` | Per-user key |
| `internal` | System/AI use (ik_ prefix) |

## Environments

- `live` — Production data
- `test` — Sandbox data (key includes sandbox slug)

## Embed Tokens (separate from API keys)

Embed tokens authenticate client-side widgets. They are not API keys and cannot be used with the API.

| Prefix | System | Table |
|--------|--------|-------|
| `emb_` | Loyalty SDK | `embed_tokens` |
| `hive_tok_` | Hive SDK | `hive_embed_tokens` |

## Agent M2M Tokens

Autonomous agents use Stytch M2M OAuth2 `client_credentials` grant. Access tokens are standard JWTs — no Bagdock-specific prefix.

## Dashboard

Manage API keys at `/{operatorSlug}/developer/keys` in the operator dashboard.

# API Keys

Bagdock API keys are operator-scoped and used for programmatic access.

## Key Types

| Type | Prefix | Access |
|------|--------|--------|
| Secret | `bdok_sk_` | Full API access, server-side only |
| Publishable | `bdok_pk_` | Limited client-side access |

## Endpoints

### Create API Key

```
POST /v1/operator/api-keys
```

Body:
```json
{
  "name": "CI Deploy Key",
  "type": "secret",
  "category": "standard",
  "environment": "live",
  "scopes": ["apps:deploy", "apps:read"]
}
```

Response includes the raw key (shown once):
```json
{
  "data": {
    "id": "bdok_key_xxx",
    "rawKey": "bdok_sk_live_xxxxxxxxxxxxx"
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

## Environments

- `live` — Production data
- `test` — Sandbox data

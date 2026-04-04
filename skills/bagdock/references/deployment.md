# Deployment

Bagdock deploys apps and edges to Cloudflare Workers for Platforms. Developers push compiled bundles via the API; the platform handles CF credentials and namespace management.

## Environments

| Environment | URL Pattern | Namespace | Notes |
|-------------|-------------|-----------|-------|
| Production | `{slug}.bdok.dev` | `bagdock-adapters-prod` | Requires review for public apps |
| Staging | `{slug}.pre.bdok.dev` | `bagdock-adapters-staging` | Stable pre-production |
| Preview | `{slug}-{hash}.pre.bdok.dev` | `bagdock-adapters-staging` | Ephemeral, per-deploy |

## Deploy via CLI

```bash
bagdock deploy                    # Default: staging
bagdock deploy --production       # Production (requires approval for public)
bagdock deploy --preview          # Ephemeral preview
bagdock deploy --env staging      # Explicit environment
```

## Deploy via API

```bash
curl -X POST "https://api.bagdock.com/v1/developer/apps/my-adapter/deploy" \
  -H "Authorization: Bearer $BAGDOCK_API_KEY" \
  -F "script=@dist/worker.mjs" \
  -F 'metadata={"version":"1.0.0","environment":"staging"}'
```

## Version History

Each deploy creates a version record in `integration_adapter_versions` with:
- Environment
- Compatibility date
- Deployed timestamp
- CF script name
- Worker URL
- Preview hash (for preview deploys)

Query version history:
```
GET /v1/developer/apps/:slug/versions
```

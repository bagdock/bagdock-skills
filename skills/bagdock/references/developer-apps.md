# Developer Apps API

The Developer Apps API manages the lifecycle of apps and edges on the Bagdock platform.

## Create App

```
POST /v1/developer/apps
```

```json
{
  "slug": "my-adapter",
  "name": "My Adapter",
  "type": "access_control",
  "category": "full_access",
  "visibility": "private",
  "config": { "auth_type": "api_key" }
}
```

## Deploy

```
POST /v1/developer/apps/:slug/deploy
Content-Type: multipart/form-data
```

Fields:
- `script` — Compiled Worker JS file (ES module)
- `metadata` — JSON: `{ "version": "1.0.0", "environment": "staging", "compatibilityDate": "2024-09-23" }`

### Governance

- Private apps: deploy freely to any environment
- Public integrations: preview/staging freely; production requires `review_status = 'approved'`

## Environment Variables

Variables are stored in the platform secret manager and synced to the Worker on deploy.

- `GET /v1/developer/apps/:slug/env` — List keys (values not exposed)
- `PUT /v1/developer/apps/:slug/env` — Set key/value
- `DELETE /v1/developer/apps/:slug/env/:key` — Remove

## Submission Lifecycle

- `POST /v1/developer/apps/:slug/submit` — Submit for review (draft -> submitted)
- `GET /v1/developer/apps/:slug/submissions` — List submission history
- `GET /v1/developer/apps/:slug/submissions/:id` — Submission detail
- `POST /v1/developer/apps/:slug/submissions/:id/withdraw` — Withdraw (submitted -> draft)

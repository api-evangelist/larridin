# Larridin

Larridin is an enterprise AI intelligence platform that measures whether an organization's investment in AI is actually paying off across both its human and agent workforce. Its Scout product instruments AI usage through a managed browser extension and desktop agent, then joins that telemetry with source control, coding-assistant, incident, and work-tracking systems to report on AI adoption, AI fluency, AI governance and shadow-tool risk, token spend, workflow intelligence, and Developer Intelligence.

- Website — https://larridin.com/
- Developer docs — https://docs.larridin.com/
- Scout API v1 reference — https://docs.larridin.com/api/scout-api-v1-reference
- MCP server (beta) — https://docs.larridin.com/api/mcp
- Trust Center — https://trust.larridin.com/

Backed by: bloomberg-beta, homebrew

## APIs

| API | Base URL | Spec |
|---|---|---|
| Larridin Scout API v1 | `https://scout-api.larridin.com/api/v1` | [`openapi/larridin-scout-openapi.yml`](openapi/larridin-scout-openapi.yml) |

The Scout API v1 is read-only: all 41 documented operations are `GET`. Authentication is a company API key in the `x-company-api-key` header, which must carry the `ANALYTICS` scope. The beta MCP server is separately authenticated with OAuth 2.0.

## Artifacts

| Artifact | Path | Method |
|---|---|---|
| OpenAPI 3.1 | `openapi/larridin-scout-openapi.yml` | generated from the public reference |
| MCP server | `mcp/larridin-mcp.yml` | searched |
| llms.txt | `llms/larridin-llms.txt` | searched (verbatim) |
| Well-known | `well-known/` | searched |
| Authentication | `authentication/larridin-authentication.yml` | searched |
| OAuth scopes | `scopes/larridin-scopes.yml` | searched |
| Conventions | `conventions/larridin-conventions.yml` | searched |
| Error catalog | `errors/larridin-problem-types.yml` | searched |
| Lifecycle | `lifecycle/larridin-lifecycle.yml` | searched |
| Conformance | `conformance/larridin-conformance.yml` | searched |
| Trust center | `security/larridin-trust-center.yml` | searched |
| Vulnerability disclosure | `security/larridin-vulnerability-disclosure.yml` | searched |
| Domain security | `security/larridin-domain-security.yml` | probed |
| Data model | `data-model/larridin-data-model.yml` | derived |
| Agentic access | `agentic-access/larridin-agentic-access.yml` | generated |
| Overlay | `overlays/larridin-scout-overlay.yaml` | generated |
| Agent Skills | `skills/` | generated |

## Notes

Larridin publishes a human-readable API reference but no machine-readable OpenAPI description — the spec here is a faithful transcription by the API Evangelist enrichment pipeline, not a provider-published artifact. No SDKs, CLI, sandbox, changelog, status page, deprecation policy, pricing page, or event/webhook surface were found on the public developer surface as of 2026-07-19.

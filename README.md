# Larridin

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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

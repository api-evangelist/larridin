---
name: Audit shadow AI and policy enforcement
description: Use the Larridin Scout API to inventory unapproved AI tools in use, review how policy enforcement is landing, and trace usage down to the tool and user level for a governance review.
api: openapi/larridin-scout-openapi.yml
generated: '2026-07-19'
method: generated
source: https://docs.larridin.com/api/scout-api-v1-reference
operations:
  - getToolsUnapprovedOverview
  - getToolsUnapprovedBreakdown
  - getToolsPolicyEnforcementOverview
  - getToolsPolicyEnforcementBreakdown
  - getToolsPolicyBreakdown
  - getToolsByToolid
  - getToolsUserToolUsage
---

# Audit shadow AI and policy enforcement

Use this skill to answer "what unsanctioned AI is being used here, and is our policy actually holding?"

## Before you start

- Base URL is `https://scout-api.larridin.com/api/v1`.
- Send the company API key in the `x-company-api-key` header, with the `ANALYTICS` scope.
- Everything here is a read-only `GET`.
- This data is about identifiable employees. Treat the user-level step as sensitive and only pull it when
  the review genuinely requires it.

## Steps

1. **Size the shadow surface.** Call `getToolsUnapprovedOverview` for the headline count of unapproved AI
   tool usage in the window.

2. **List the offending tools.** Call `getToolsUnapprovedBreakdown` to get the per-tool breakdown. Tool
   records carry `toolId`, `name`, `category`, `status`, `platform`, and `licenseType`.

3. **Check enforcement.** Call `getToolsPolicyEnforcementOverview` for the summary of how policy is being
   enforced, then `getToolsPolicyEnforcementBreakdown` for the per-item detail. Use `getToolsPolicyBreakdown`
   for the policy-level cut.

4. **Drill into a specific tool.** With a `toolId` from step 2 or 3, call `getToolsByToolid` for that
   tool's metrics over time. Confirm `status` — `APPROVED` versus otherwise — before you escalate it as
   shadow usage.

5. **Attribute usage, if the review requires it.** Call `getToolsUserToolUsage` for user-level AI tool
   usage. Filter with bracket notation to keep the pull tight:
   `?department[]=dept-123&tool[]=tool-456&platform[]=BROWSER`.

6. **Split browser versus desktop where it matters.** `getToolsBrowserOverview` / `getToolsBrowserBreakdown`
   and `getToolsDesktopOverview` / `getToolsDesktopBreakdown` separate the two collection paths. Note that
   the desktop breakdown is tools-only — it does not support department grouping.

## Reading the response

Responses use `{ "success": true, "data": {...}, "query": {...} }`. Breakdown endpoints paginate via
`page` / `limit` (default 10, max 100) and return `total`, `page`, and `limit`.

Do not read a **missing** field as zero — missing means "not applicable for these parameters", while
`null` means "no data for this period". Misreading that difference will overstate or understate a
governance finding.

## Errors

- `400` — validation failed; inspect `details[]`.
- `401` — key missing, invalid, or lacking `ANALYTICS`.
- `404` — the `toolId` does not belong to your organization.
- `500` — retry, then escalate.

Full catalog: `errors/larridin-problem-types.yml`. Cross-cutting rules: `conventions/larridin-conventions.yml`.

---
name: Review workflow friction and tool impact
description: Use Larridin Workflow Intelligence to find where work is getting stuck, which tools help or hurt, and what the platform recommends changing.
api: openapi/larridin-scout-openapi.yml
generated: '2026-07-19'
method: generated
source: https://docs.larridin.com/api/scout-api-v1-reference
operations:
  - getWorkflowCompletedPeriods
  - getWorkflowOverview
  - getWorkflowWorkflows
  - getWorkflowWorkflowsByWorkflowid
  - getWorkflowRecommendations
  - getWorkflowReportingGroups
  - getWorkflowAiBreakdown
  - getWorkflowAiCategoryOutcomeBreakdown
  - getWorkflowToolsOverview
  - getWorkflowToolsSearch
  - getWorkflowToolsByToolid
  - getWorkflowToolsByToolidVerdict
  - getWorkflowToolsByToolidFrictions
  - getWorkflowToolsByToolidWorkflows
---

# Review workflow friction and tool impact

Use this skill to answer "where is work getting stuck, and is AI actually helping?"

## Before you start

- Base URL is `https://scout-api.larridin.com/api/v1`.
- Send the company API key in the `x-company-api-key` header, with the `ANALYTICS` scope.
- Everything here is a read-only `GET`.
- Workflow Intelligence is period-based, not free-range-date-based. **Always start with step 1** — asking
  for an incomplete period yields empty or misleading results.

## Steps

1. **Find a valid period.** Call `getWorkflowCompletedPeriods` to get the most recent four-week periods
   that have completed. Use one of these for every subsequent call.

2. **Get the summary.** Call `getWorkflowOverview` for the org-level, or reporting-group-scoped, workflow
   picture for that period.

3. **See where AI is landing.** Call `getWorkflowAiBreakdown` for AI versus non-AI clustered-workflow
   counts and AI impact, then `getWorkflowAiCategoryOutcomeBreakdown` for the outcome distribution split
   by category.

4. **List the workflows.** Call `getWorkflowWorkflows` for a paginated breakdown of clustered workflows.
   Page with `page` / `limit` and sort with `sortBy` / `sortOrder`.

5. **Open one workflow.** With a `workflowId` from step 4, call `getWorkflowWorkflowsByWorkflowid` for its
   detailed metrics, recommendations, and step sequence.

6. **Rank the friction by group.** Call `getWorkflowReportingGroups` for a paginated, sortable breakdown
   of workflow friction by reporting group. This is usually the fastest route to "who should we go talk
   to".

7. **Judge the tools.** Call `getWorkflowToolsOverview` for tool usage and friction across all tools, or
   `getWorkflowToolsSearch` to search and page through them. Then for a specific `toolId`:
   - `getWorkflowToolsByToolid` — the tool's detailed metrics
   - `getWorkflowToolsByToolidVerdict` — the AI-impact verdict and recommendation
   - `getWorkflowToolsByToolidFrictions` — friction-type tallies for workflows using the tool
   - `getWorkflowToolsByToolidCategoryOutcome` — outcome distribution for those workflows
   - `getWorkflowToolsByToolidWorkflows` — paginated workflows comparing usage with and without the tool

8. **Collect the recommendations.** Call `getWorkflowRecommendations` for the paginated list of workflow
   improvement recommendations. Lead the write-up with these — they are the platform's own conclusions.

9. **Only if you need per-user detail.** `getWorkflowRawWorkflows` returns raw per-user, per-day
   workflows. This is sensitive; pull it only when the review genuinely requires it.

## Reading the response

Responses use `{ "success": true, "data": {...}, "query": {...} }`. Paginated endpoints return `total`,
`page`, and `limit` alongside `data`; default `limit` is 10 and the max is 100. Array filters use bracket
notation.

`null` means "no data for this period"; a **missing** field means "not applicable for these parameters".
Do not conflate either with zero friction.

## Errors

- `400` — validation failed; inspect `details[]`. Most often an incomplete period from skipping step 1.
- `401` — key missing, invalid, or lacking `ANALYTICS`.
- `404` — the `workflowId` or `toolId` does not belong to your organization.
- `500` — retry, then escalate.

Full catalog: `errors/larridin-problem-types.yml`. Cross-cutting rules: `conventions/larridin-conventions.yml`.

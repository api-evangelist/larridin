---
name: Report AI adoption across the organization
description: Pull org-wide and per-department AI adoption from the Larridin Scout API — headline metrics, the trend line, and the department or tool breakdown — and assemble them into an adoption report.
api: openapi/larridin-scout-openapi.yml
generated: '2026-07-19'
method: generated
source: https://docs.larridin.com/api/scout-api-v1-reference
operations:
  - getAdoptionOverview
  - getAdoptionTrends
  - getAdoptionBreakdown
---

# Report AI adoption across the organization

Use this skill to answer "how widely is AI actually being used here, and where is it going?"

## Before you start

- Base URL is `https://scout-api.larridin.com/api/v1`.
- Send the company API key in the `x-company-api-key` header. The key must carry the `ANALYTICS` scope.
- Every operation is a read-only `GET`. Nothing here mutates state, so retries are safe.
- Pick `startDate` and `endDate` in `YYYY-MM-DD` form. `startDate` must be `<=` `endDate`, and `startDate`
  cannot be more than one day in the future.

## Steps

1. **Get the headline numbers.** Call `getAdoptionOverview` with `startDate` and `endDate`. Leave
   `groupBy` at its default `none` for org-wide totals. Read `activeUsersCount`, `aiActiveUsersCount`,
   `aiAdoptionRate`, and the matching `*Change` fields for period-over-period movement.

2. **Get the same cut per department.** Call `getAdoptionOverview` again with `groupBy=departments`.
   Sort with `sortBy` (`aiActiveSessions`, `aiActiveUsers`, `avgDau`, `avgAiAdoptionRate`, or
   `departmentName`) and `sortOrder` to rank departments.

3. **Get the trend line.** Call `getAdoptionTrends`. `groupBy` is **required** here — use `none` for a
   single org-wide series, or `tools` / `departments` to split it. Set `granularity` to match the report
   window: `daily` for short ranges, `weekly` or `four-weekly` for a quarter, `monthly` or
   `twelve-weekly` for a year.

4. **Get the ranked breakdown.** Call `getAdoptionBreakdown` with a required `groupBy` of `tools` or
   `departments`. This endpoint paginates: pass `page` (default 1) and `limit` (default 10, max 100),
   and read `total`, `page`, and `limit` back from the response to decide whether to fetch more.

5. **Narrow if asked.** All three endpoints accept bracket-notation array filters:
   `?department[]=dept-123&department[]=dept-456`, plus `tool[]`, `platform[]` (`BROWSER` or `DESKTOP`),
   and `aiTypes[]`.

## Reading the response

Every response is the standard envelope: `{ "success": true, "data": {...}, "query": {...} }`. Read your
payload from `data`; `query` echoes the parameters the API actually resolved, which is the fastest way to
confirm a filter was applied.

Field semantics matter here and are easy to get wrong:

- A field set to `null` means the metric exists but has **no data** for that period.
- A **missing** field means the metric does not apply to the parameters you sent — for example, WAU
  metrics do not appear at `daily` granularity. Do not report a missing field as zero.
- `*Change` and `*ChangePct` are `null` when there is no prior period to compare against.

## Errors

- `400` — validation failed. Read `details[]` for the `field` and `message`. Usually a bad date order, a
  future `startDate`, or a `granularity` this endpoint does not accept.
- `401` — missing or invalid key, or the key lacks the `ANALYTICS` scope.
- `500` — retry, then escalate.

Full catalog: `errors/larridin-problem-types.yml`. Cross-cutting rules: `conventions/larridin-conventions.yml`.

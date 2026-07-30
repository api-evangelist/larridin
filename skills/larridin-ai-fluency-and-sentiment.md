---
name: Measure AI fluency and pair it with survey sentiment
description: Pull Larridin AI proficiency scores, prompt categories, and conversation metrics for a period, then pair the behavioral picture with survey responses to explain the number.
api: openapi/larridin-scout-openapi.yml
generated: '2026-07-19'
method: generated
source: https://docs.larridin.com/api/scout-api-v1-reference
operations:
  - getProficiencyScore
  - getProficiencyTrends
  - getProficiencyPromptCategories
  - getProficiencyConversationMetrics
  - getSurveys
  - getSurveysBySurveyId
  - getSurveysBySurveyIdQuestions
  - getSurveysBySurveyIdQuestionsByQuestionIdOptions
  - getSurveysBySurveyIdQuestionsByQuestionIdResponses
---

# Measure AI fluency and pair it with survey sentiment

Use this skill to answer "how *skillfully* is our organization using AI — and what do people say about
it?"

## Before you start

- Base URL is `https://scout-api.larridin.com/api/v1`.
- Send the company API key in the `x-company-api-key` header, with the `ANALYTICS` scope.
- Everything here is a read-only `GET`.
- **Proficiency endpoints do not take date ranges.** They use period selection: `periodType`
  (`monthly` or `quarterly`), `period` (1-12 for monthly, 1-4 for quarterly), and `year` — all required.
- Proficiency accepts only `weekly` or `biweekly` for `granularity`, not the full granularity set.

## Steps

1. **Get the score.** Call `getProficiencyScore` with `periodType`, `period`, and `year`. Read
   `aiProficiencyScore` plus its three components — `promptQualityComponent`,
   `featureAdoptionComponent`, and `useCaseDiversityComponent` — and the percentile spread
   (`p25`/`p50`/`p75`/`p85`). `prevPeriodValue` and `prevPeriodDelta` give the movement.

2. **Break it out by department.** Call `getProficiencyScore` again with `groupBy=departments` to see
   which teams are pulling the average up or down.

3. **Get the trend.** Call `getProficiencyTrends` for the time series. Request percentile bands with
   `percentiles[]=p25&percentiles[]=p50&percentiles[]=p75` — a rising average with a flat p25 means the
   already-strong users are improving and everyone else is not, which is a different problem.

4. **See what people use AI for.** Call `getProficiencyPromptCategories` for the topic/prompt
   classification breakdown. Filter with `topics[]` to focus. This is where "high adoption, low value"
   shows up.

5. **Check interaction depth.** Call `getProficiencyConversationMetrics` for `avgTurnDepth`,
   `singleTurnDominancePct`, and `messagesPerSession`. High single-turn dominance usually means people are
   treating AI as a search box rather than working with it.

6. **Pair it with what people say.** Call `getSurveys` for the paginated list of survey campaigns, then
   `getSurveysBySurveyId` for one campaign, `getSurveysBySurveyIdQuestions` for its questions,
   `getSurveysBySurveyIdQuestionsByQuestionIdOptions` for a question's options, and
   `getSurveysBySurveyIdQuestionsByQuestionIdResponses` for the answers.

7. **Write it up.** Lead with the score and its trend, explain it with the component breakdown and prompt
   categories, and use the survey responses as the qualitative counterpart.

## Reading the response

Responses use `{ "success": true, "data": {...}, "query": {...} }`. Proficiency payloads also carry
`filters`, `groupedByDepartment`, and a `summary` with the resolved `dateRange` — check that `dateRange`
to confirm which calendar window your period actually mapped to. `pendingPeriod` flags a period still in
progress.

`null` means "no data for this period"; a **missing** field means "not applicable for these parameters".

## Errors

- `400` — validation failed; inspect `details[]`. Usually a `period` out of range for the `periodType`,
  or a `granularity` other than `weekly` / `biweekly`.
- `401` — key missing, invalid, or lacking `ANALYTICS`.
- `404` — the `survey_id` or `question_id` does not belong to your organization.
- `500` — retry, then escalate.

Full catalog: `errors/larridin-problem-types.yml`. Cross-cutting rules: `conventions/larridin-conventions.yml`.

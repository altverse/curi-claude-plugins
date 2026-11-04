---
name: signal-survey
description: Use when the user wants to create, check, publish or read the results of a survey or interview in signal (askcuri.com) — drafts come from the AI draft job, publishing needs the user's go-ahead.
---

# Running a survey in signal

1. Start from the goal: ask who should answer and in which language if the user hasn't said. Then `create_survey_draft` (goal, audience, language; add `material_url` or `material_text` when the user gives source material). If it returns `team.required`, ask which of the listed teams to use and pass `team_uuid`.
2. The draft is written in the background. Check progress with `get_survey` — `generation.status` goes `queued` → `running` → `done` (or `failed` with a reason). Share the `editor_url`; the user reviews and edits there.
3. Publish only when the user says so. `publish_survey` needs `confirm_title` equal to the survey's current title (read it with `get_survey`). Share the returned `respondent_url`.
4. Results: `list_surveys` → `get_results` for counts, completion, drop-off and coded themes. Free-text answers and quotes come back masked; don't try to identify respondents.
   For a survey with many responses, `get_results` can be slow. Then call `start_results` (same `survey_uuid` and `ver`) instead. It returns a `job_id` at once. Call `get_job` with that `job_id` every `poll_after_seconds` (3 seconds) while `status` is `queued` or `running`. When `status` is `done`, `result` holds the same body as `get_results`. When it is `failed`, tell the user the `error_code`. Most jobs finish within a minute. A job is kept for one day and only the account that started it can read it; if `get_job` returns `mcp.job_not_found`, call `start_results` again.
5. Report: `get_report_pdf_link`. If it returns `queued` or `running`, tell the user it's being built and check again a little later; a `ready` link works for 15 minutes.

Plans: every plan (Free included) can read and draft through the connector — a draft only uses the question types the plan allows, and anything left out is listed with an upgrade note. Publishing through the connector is included from Starter up; on Free, publish from the signal editor instead. If a tool returns `billing.feature_not_in_plan`, tell the user their plan doesn't include it and share the `billing_url` it returns.

A new account with no team gets an example team with one sample survey and synthetic responses. There you can read everything and draft up to three surveys a day, but publishing is turned off (`mcp.example_publish`).

The connector can't delete surveys, send messages to respondents, or see contact details. It acts with the user's role in each team (viewer can read; editor or owner can draft and publish).

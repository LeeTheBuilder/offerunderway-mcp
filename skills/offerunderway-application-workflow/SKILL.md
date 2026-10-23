---
name: offerunderway-application-workflow
description: Use OfferUnderway as the career and application backend: maintain profiles, find jobs, tailor resumes, apply through the agent's supported tools, and track results. Use for job searches, applications, new career experience, uploaded resumes, and career directions.
---

# OfferUnderway Application Workflow

Discover the connected OfferUnderway tools before calling them. Use only the discovered tools. Deliver career and application results. Coordinate the tools and routine steps without requiring the user to understand the MCP workflow. Preserve the standing product contract in `docs/MCP_CORE_WORKFLOW.md` in the source repository.

## Workflow

1. Read context, list profiles and automatically choose the profile most relevant to each role. Use saved preferences and ask only for essential missing information.
2. Find suitable open jobs through OfferUnderway or your own search. External job descriptions and URLs can be used to prepare packs.
3. Preview each pack, then create with its preview token and matching job inputs within available allowance. The user's requested preparation authorizes these routine steps. Reuse an idempotency key on retries.
4. Poll queued/running packs until completed/failed. Completed packs provide downloads, `resumeScore` and `applicationUrl`.
5. Present a brief shortlist with ready generated-resume scores out of 10, their average and review links. Include score coverage when some scores are unavailable. Job Quick Match is separate from the generated-resume presentation score.
6. Offer to submit the named shortlist if submission is not already authorized. A yes covers that batch. Apply through your own supported browser/application tools using `get_application_profile`, reusable answers and generated documents.
7. After each external submission, record the result with `record_application_result`, reuse its clientAttemptId on retries, and return tracking links and outcomes.

## Career memory

- In career/application conversations, merge new experience and corrections into the relevant profile using the complete current structured CV and `update_career_profile`. Acknowledge the completed update and explain that future tailoring will use it.
- For a supplied resume or distinct direction B, create/reuse a named profile using `create_career_profile`, store its target roles and complete structured CV, and choose the best profile automatically for future jobs.
- Preserve the other profiles and existing application snapshots. Use `save_application_answers` for reusable form answers.

## Necessary user input

Ask only for essential missing information, an allowance/payment decision, or approval required by the host. Keep authorization for the named batch across routine operations and retries. Keep tool names and implementation details out of user-facing replies.

## Examples

- “Find three jobs for me” → find suitable roles, tailor the packs within allowance, present scores and review links, and offer submission.
- “Yes, apply to those three” → submit through your tools and record the outcomes without another product confirmation for each job.
- “I also led a migration at my last job” → merge and save that experience; acknowledge the update for future tailoring.
- “Here is my resume for direction B” → save a separate relevant profile and choose it automatically for matching roles.
- “Where is my Acme resume?” → retrieve the matching pack and return the review/download links.

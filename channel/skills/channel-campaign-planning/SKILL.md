---
name: channel-campaign-planning
description: Use when the user wants to plan or draft an email campaign, topic, or social post in channel (askcuri.com) — check audience first, then create drafts; never claims to send.
---

# Planning a campaign in channel

1. Find or create the topic: `list_topics` → `get_topic`; if none fits, `create_topic` with a clear goal.
2. Check the audience before writing: `search_subscribers` (counts by region/source/tag). Ask for emails only if the user needs specific people (`include_emails`).
3. Look at what worked: `list_campaigns` / `get_campaign` for past subject lines and results; `get_trend_report` if one exists.
4. Draft: `create_campaign_draft` (name, subject, HTML content, topic). Offer 2 subject-line options in chat.
5. Revise with `update_campaign_draft` until the user is happy.
6. Hand off: share the `editUrl`. Sending and scheduling happen in channel web — say so plainly; don't imply the email was sent.

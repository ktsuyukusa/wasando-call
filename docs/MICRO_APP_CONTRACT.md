# WaSanDo Micro-App Contract

Every WaSanDo app has **one job**.

## Product rule
If the product description needs “and” to explain its primary purpose, split it.

A micro-app must:
- solve one clearly named business problem;
- produce one primary business result;
- work and be sellable independently;
- expose its result so another app can consume it immediately;
- never require another WaSanDo app to perform its core job.

## Integration rule
Integration is a capability of every app, not a reason to merge apps.

Each app exposes a stable integration boundary:
1. **Events** — what happened (`call.completed`, `lead.created`).
2. **Actions** — what another app may request.
3. **Data contract** — versioned JSON objects with IDs and timestamps.
4. **Webhooks/API** — optional outbound webhook and authenticated API adapter.
5. **Import/export** — JSON/CSV where practical.
6. **Identity** — `tenant_id`, `customer_id`, and source IDs allow records to join without sharing internal databases.

No app reads another app’s private database directly.

## WaSanDo CALL
**One purpose:** answer the company reception telephone number.

Input: incoming telephone call.
Output: completed reception record.

Canonical output fields: schema, tenant_id, call_id, caller, started_at, ended_at, language, intent, summary, urgency, next_action, transcript_ref, recording_ref.

CALL does not become a CRM, website builder, social publisher, SMS campaign tool, quotation system or booking system. Those are separate apps. CALL may hand its output to any of them.

## Plug-in examples
CALL -> Booking
CALL -> Quote Intake
CALL -> Follow-up
CALL -> Customer Record
CALL -> Revenue Measurement

Number Migration -> SMS Notice
Number Migration -> Website Number Update
Number Migration -> Social Announcement

The arrow is an integration contract, not shared product code.

## White-label and localization
Brand, language, industry knowledge, telephony provider and deployment settings are configuration layers. Customer-specific code must not enter the core.

## Test for every new feature
1. Is this required to complete this app’s one job?
2. If not, can it be a separate app receiving an event?
3. Can a third-party system replace that app without changing this app?

If #1 is no, split it. If #3 is no, the integration is too tightly coupled.

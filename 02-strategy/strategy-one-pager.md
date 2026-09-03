# AI Strategy One-Pager - Juno Automated Prioritization

## 1. Problem & Workflow

The Problem: roadmap discussions at RocketShip are driven by the loudest voice in Slack rather than customer evidence. Priorities reverse weekly; stakeholder trust is eroding.

Prevention: Juno explicitly prevents 'opinion-driven prioritization' - the bad decision of moving a feature up the backlog because someone in #leadership posted strongly, instead of because the cited evidence outweighs the alternatives.

## 2. Target Metrics

Cycle time: reduce average weekly roadmap prioritization from 2 hours to 30 minutes (75% reduction).

Leadership proof: under-10% rate of decisions reversed within 1 week, AND 90%+ of prioritised items have at least 2 cited sources from the corpus. Both metrics measurable in the first 30 days post-launch.

## 3. Autonomy Level

Choice: Copilot. Juno drafts a ranked backlog with written reasoning + source citations; the PM reviews and clicks 'approve' before publish.

Explicitly avoiding: Agent. Letting Juno move sprint priorities or shift live dates without a human approval step is a one-way trust-erosion door - a single wrong call lets stakeholders dismiss the system permanently.

## 4. Data & Model Approach

Approach: Ground (RAG). We will ground the model in the RocketShip corpus - Slack #escalations, support tickets, interview notes, Notion product pages, Jira tickets - so every priority cites a source ID.

Explicitly avoiding: a generic LLM (Buy). Without RAG grounding, Juno would hallucinate plausible-sounding priorities and invent customer signals that don't exist - the failure mode that kills trust fastest.

## 5. Risks & Mitigations

Risk: training data lag. Juno could over-weight whichever signal type was loudest in the past 60 days (e.g. enterprise escalations) and systematically under-weight quieter but more strategic signals (e.g. SMB churn). One quarter of skewed priorities and the roadmap drifts.

Mitigation: a hard 'evidence balance' eval gate - reject any priority list where less than 20% of cited sources come from any one source type. Run weekly; PM reviews.

## 6. V1 Scope

In: ranking the existing backlog with cited evidence; surfacing under-cited items; flagging conflicts between Slack escalations and Jira priorities.

Out: (1) hiring or headcount decisions, (2) customer-facing comms about why a feature was deprioritised. Both stay 100% with the human PM.


## Diagnostic Diff · Juno RAG Lab

**Prototype:** https://ai-pm-synthesizer.lovable.app

### Before, Quality Mode (no strategy)

P1 “But then, and this is the part that makes me want to scream, I try to click ‘Export to CSV’ because I need to pivot this in Excel.” Medium
Neutral
Interview
Reporting

P2 “It spins for like 5 minutes and then just crashes.” Medium
Negative
Ticket
Performance
 
P3 “I’ve lost hours because of this.” Medium
Negative
Interview
General

### After, Strategy Mode (with RocketShip Strategy One-Pager)

P0
Reliability First
100/100
Resolve CSV Export Timeouts for Large Date Ranges
Reports export to CSV is timing out on date ranges over 90 days, blocking finance workflows during quarterly reporting.

The strategy explicitly designates CSV export stability as a non-negotiable goal under 'Reliability First' ('P0 reliability bugs - CSV export crashes... ZERO new feature work ships if the legacy reporting API is redlining'). Decision rules state workflow blockers like CSV crashes are P0/P1.
--------

P0
Enterprise Compliance
90/100
Streamline Team Invites and Role Setup for Enterprise Accounts
Acme Corp was blocked during onboarding for two days trying to invite team members and manage initial access.

The strategy highlights Acme Corp as a critical enterprise account ('Acme deal worth $200k ARR') and prioritizes user management and role-based permissions under 'Enterprise Compliance'. Unblocking team onboarding directly protects this revenue.
--------

P2
Reliability First
65/100
Investigate Notification and Alert Delivery Failures
Users report intermittent alert delivery, causing missed notifications over the past week.

While aligned with 'Reliability First' ('The platform must work. Every export, every report, every load'), alert reliability is secondary to critical export crashes and enterprise SSO blockers.

### Takeaway

> RAG makes the quality of information so much more reliable and reduces allucinations/mistakes.

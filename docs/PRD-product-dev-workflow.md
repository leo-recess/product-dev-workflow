# Product Development Workflow System — Full PRD

> **Size:** XL (multi-phase, multi-system)
> **Type:** Full feature — internal ops infrastructure
> **Date:** 2026-03-10
> **Status:** Pending COO Approval

---

## 1. GOALS AND OBJECTIVES

**Primary goal:** Build a complete product development workflow system that gives the COO full visibility and planning control while giving the developer automated task capture, clear priorities, and minimal board maintenance.

**Secondary goals:**
- Eliminate manual Asana data entry — all tasks enter via Asana Form (V1), Slack `/backlog` (V2), or meeting transcripts
- Automate project creation, task routing, and weekly board operations
- Create a single source of truth across Pipeline, Active Work, and Feature Projects
- Establish size-based routing so small work ships fast and large work gets proper scoping

---

## 2. TARGET AUDIENCE

**Primary audience:** COO (planning, visibility, approvals) and Developer (execution, task management)

**Secondary audience:** Any team member who submits work via Asana Form or Slack `/backlog` command

**How many people this affects:** 2 core users (COO + Dev), ~5-10 team members submitting requests

---

## 3. PROBLEM STATEMENT

Today, work enters through scattered channels — Slack messages, meetings, ad-hoc requests. There's no consistent intake process, no size-based routing, no automated board management, and no way for the COO to see a unified view of what's planned, in progress, or blocked. Meeting action items get lost. Small bugs and large projects follow the same (or no) process. The developer spends time on board hygiene instead of building.

**Cost of not solving:** Missed tasks, unclear priorities, COO flying blind on progress, scope creep on large projects, meeting follow-ups falling through cracks.

---

## 4. CREATIVE / UNIQUE TAKE

The system is designed around **one principle: automation handles the glue**. Instead of forcing humans to maintain boards, route tasks, or create project structures, every repetitive workflow action is automated. The COO plans and approves. The developer builds. Everything in between — intake, routing, board updates, project scaffolding, meeting follow-up — runs itself.

Key differentiator: A single "Active Work" dropdown field on any task, in any project, controls whether it appears on the unified Active Work board. No manual multi-homing. No copying tasks between projects.

---

## 5. PROPOSED SOLUTION — HIGH LEVEL

**From the COO's perspective:**
- Open Asana Portfolio → see all active projects, their phases, and status
- Open Active Work board → see everything being worked on this week, what's blocked, what's in review, what just completed
- Rank the backlog → developer knows exactly what to pull next
- Get Slack notifications when projects are created, tasks complete, or meetings generate action items
- Review PRDs and approve scope for L/XL work before building starts

**From the Developer's perspective:**
- See a ranked list of what to work on next
- Set "Active Work = This Week" on any task → it appears on the board automatically
- Tasks from Slack and meetings show up pre-formatted with AI-generated titles, descriptions, and size suggestions
- Monday morning: "Next Week" tasks automatically roll to "This Week"
- Completed tasks auto-archive after 10 days

**From any team member's perspective:**
- Submit work via Asana Form (V1) or type `/backlog` in any Slack thread (V2) → task appears in Asana Pipeline with full context

---

## 6. CHANNELS AND DISTRIBUTION

- **Asana Form** — V1 intake channel (built into Pipeline & Backlog project)
- **Slack** — V2 intake channel (`/backlog` command, available in all channels)
- **Asana** — primary execution and visibility platform (Portfolio, Pipeline, Active Work, Feature Projects)
- **Fireflies + Make.com** — meeting transcript capture and processing
- **Adoption:** Roll out Asana structure + Form to COO + Developer first (Phase 1), then enable Slack `/backlog` for full team (Phase 2), then transcript automation (Phase 3)

---

## 7. SUCCESS METRICS AND KPIs

- **KPI 1:** 100% of new work enters via Form, `/backlog`, or transcript automation (zero manual Asana entry) — target within 30 days of launch
- **KPI 2:** COO can see real-time status of all active work in <10 seconds (Active Work board accuracy) — target at launch
- **KPI 3:** Average time from Slack request to Asana task < 2 minutes (automated intake speed) — target at Phase 2 launch
- **KPI 4:** Zero missed meeting action items (transcript extraction captures all) — target within 60 days
- **When do we measure:** 30 days post-launch for intake adoption, 60 days for transcript accuracy calibration

---

## 8. STAKEHOLDERS AND ROLES

- **Business owner (PRD author):** COO
- **COO reviewer:** COO (self — owns Pipeline & Backlog)
- **Developer:** Leo (owns Active Work board + all automation builds)
- **Final sign-off:** COO + Leo jointly

---

## 9. DEPENDENCIES AND CONSTRAINTS

**Technical dependencies:**
- Asana Business plan (required for custom fields, rules, portfolios, multi-homing)
- Slack workspace with ability to install custom apps
- Make.com account (automation orchestration)
- Claude API access (AI task generation + transcript analysis)
- Fireflies.ai account with webhook support (meeting transcription)

**Timeline constraints:** Flexible — no hard deadline. Quality over speed.

**Budget constraints:** Existing subscriptions (Asana, Slack, Make.com, Fireflies). Claude API usage costs for task generation and transcript analysis.

---

## 10. RISKS

- **Risk 1:** Asana API rate limits during bulk project creation → **Mitigation:** Batch operations, add delays between API calls
- **Risk 2:** AI-generated task titles/descriptions are low quality → **Mitigation:** Pilot with real tasks in Phase 2, calibrate prompts before full rollout
- **Risk 3:** Transcript extraction pulls false positives (non-action items flagged as tasks) → **Mitigation:** Phase 3 pilot with real meeting, human review before auto-creation, confidence thresholds
- **Risk 4:** Team doesn't adopt `/backlog` command → **Mitigation:** Make it the only intake path, deprecate DMs/ad-hoc requests

---

## 11. OUT OF SCOPE

- Daily progress updates or automated daily standups
- Time tracking or effort logging
- Client-facing dashboards or reporting
- Billing/invoicing integration
- Custom Asana UI or browser extensions
- Mobile-specific workflows

---

## FEATURE BREAKDOWN — Standalone Components

Each feature below becomes an individual Asana task when the project is approved.

---

### PHASE 1 — ASANA STRUCTURE + MVP INTAKE (Foundation)

#### F1. Portfolio Setup
Create top-level Asana Portfolio ("Product Development"). Configure portfolio-level views for COO cross-project visibility.

#### F2. Pipeline & Backlog Project
Create COO-owned project with sections: Intake → Define / PRD → Scope & Estimate → Ready → Backlog (Ranked). All work enters here.

#### F3. Active Work Project
Create Developer-owned project with sections: This Week → In Progress → In Review → Blocked → Completed This Week → Next Week.

#### F4. Custom Fields — Global
Create shared custom fields attached across all projects:
- **Size** (dropdown): XS, S, M, L, XL
- **Type** (dropdown): New Project, Bug & Quick Fix, Feature
- **Active Work** (dropdown): This Week, Next Week, Rejected, (empty)
- **Project Association** (dropdown): all active projects + "New Project"
- **Submitted By** (dropdown): each team member as an option

#### F5. Asana Form — MVP Intake (V1)
Build an Asana Form on Pipeline & Backlog project with fields:
- Task Name (required)
- Submitted By (dropdown)
- Project Association (dropdown)
- Request Type (dropdown)
- Task Description (free text)

Form submits task into Intake section of Pipeline & Backlog.

#### F6. Asana Rules — Submitted By Auto-Assignment
One Asana rule per "Submitted By" dropdown option. When Submitted By = [Person] → assign task to that person. Each team member gets their own rule.

#### F7. Asana Rules — Size-Based Auto-Skip
Native rule on Pipeline & Backlog: IF Size = XS or S → auto-move to Backlog section top. Bypasses Define/Scope stages.

#### F8. Feature Project Template
Reusable Asana project template for L/XL work:
- Standard tasks: Initiation, Scope Review, MVP Review, Completion Review
- Active Work custom field pre-attached
- Multi-home rule pre-configured
- Sections: Scope → MVP → Refinement → Completion

#### F9. Multi-Home Configuration
When Active Work dropdown = "This Week" or "Next Week" on any task in any project → task appears on Active Work board while staying in source project.

#### F10. Asana Rules — Completion & Archival
- When task completed → moves to "Completed This Week" section
- Saved filter hides completed tasks older than 10 days
- When Active Work = "Rejected" → remove from Active Work board, archive in source project

---

### PHASE 2 — AUTOMATION (Refinement)

#### F11. Slack `/backlog` Command — Bot Setup
Build Slack app with `/backlog` slash command. Opens a modal form with fields:
- Project Association (dropdown, synced from Asana)
- Request Type (dropdown)
- Link (optional URL)
- Additional Details (optional free text)

Backend captures the form submission + full parent thread context.

#### F12. AI Task Generation Backend
Claude API integration that receives Slack form + thread context and generates:
- Task title (concise, actionable)
- Task description (structured, includes thread context)
- Size suggestion (XS/S/M/L/XL)

Creates Asana task in Pipeline & Backlog Intake section with all fields populated.

#### F13. Slack Confirmation Response
After Asana task creation, post a confirmation message back to the Slack thread with task title, suggested size, and direct Asana link.

#### F14. New Project Auto-Creation
Make.com scenario triggered when a task reaches "Ready" stage AND Type = "New Project" OR Project Association = "New Project":
- Create project from Feature Project Template
- AI analyzes PRD from Pipeline task → extracts features/components → creates tasks in new project
- Add new option to "Project Association" dropdown via Asana API
- Add project to Portfolio
- Post Slack notification with project link

#### F15. Weekly Rollover Automation
Make.com scheduled scenario — Monday 8AM:
- Query all tasks where Active Work = "Next Week"
- Update each to Active Work = "This Week"

---

### PHASE 3 — INTELLIGENCE

#### F16. Transcript Webhook Integration
Connect Fireflies.ai webhook to Make.com. When a meeting transcript is ready, trigger the processing pipeline.

#### F17. AI Transcript Analysis
Claude API receives full transcript and extracts:
- Action items (with owners) → creates tasks in Active Work
- New feature requests → creates tasks in Pipeline & Backlog
- Milestones/dates → adds to relevant project sections
- Blockers → flags in appropriate tasks

#### F18. Transcript → Asana Task Creation
Make.com scenario that takes AI extraction output and:
- Creates Asana tasks in correct projects with correct fields
- Assigns owners where identified
- Sets appropriate size estimates

#### F19. Transcript Slack Summary
Posts a formatted summary to Slack after processing:
- List of created tasks with Asana links
- Action items by owner
- Any items that need manual review (low confidence extractions)

---

## REVIEW GATES

- **Scope Review:** COO approves this PRD + implementation plan before build starts
- **MVP Review (Phase 1 complete):** Asana structure live, Form intake working, rules firing correctly. COO + Dev review in existing bi-weekly.
- **Phase 2 Review:** Slack `/backlog` + automations working end-to-end. Demo with real tasks.
- **Completion Review (Phase 3 complete):** Transcript system piloted with real meeting. Full system sign-off.

---

## DO NOT EDIT BELOW — Filled in during Scope + Estimate phases

### IMPLEMENTATION PLAN:
[Developer + Claude Code create during Scope phase]

### PHASES:
- Phase 1 (MVP — Structure + Form Intake): [description] — Est: [days]
- Phase 2 (Refinement — Slack + Automations): [description] — Est: [days]
- Phase 3 (Intelligence — Transcripts): [description] — Est: [days]

### TOTAL ESTIMATE: [days]

### LAUNCH PLAN:
- Phase 1 to prod: [date] — Reviewer: COO
- Phase 2 to prod: [date] — Reviewer: COO + Dev
- Phase 3 to prod: [date] — Reviewer: COO + Dev

### POST-LAUNCH:
- Retrospective date: [date]
- KEEP / START / STOP review
- Success metric review dates: [30d, 60d]

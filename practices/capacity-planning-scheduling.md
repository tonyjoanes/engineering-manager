# Capacity Planning & Scheduling for Platform and DevOps Teams

## The Shared Team Problem

Product teams have it relatively simple: one set of stakeholders, one roadmap, one clear priority order. Platform and DevOps teams have none of this.

You serve multiple squads simultaneously. Work arrives from every direction — Squad A needs a new pipeline, Squad B has a Defender alert they don't understand, Squad C wants a Bicep module, and leadership wants a cost report by Friday. Meanwhile your team is on-call, dealing with a flaky deployment, and trying to make progress on the platform roadmap.

**The result, without a system:**
- Everything feels urgent
- Nobody knows when their thing will get done
- Your team context-switches constantly
- Stakeholders lose trust because commitments slip
- Engineers burn out

**The illusion of "just fit it in"** is the most dangerous belief in a shared team. Every "quick favour" has a real cost: switching context, losing flow, delayed planned work, and a growing sense that nothing is ever truly done.

This guide gives you the operational system to manage demand, protect your team, and give stakeholders honest, data-driven answers about when their work will get done.

**This guide assumes you've read:**
- [Planning & Prioritization](planning-prioritization.md) for RICE scoring, intake templates, and interrupt budgets
- [Stakeholder Management](../leadership/stakeholder-management.md) for communication and managing up
- [Saying No](../heuristics/saying-no.md) for boundary-setting scripts

---

## Understanding True Capacity

The basic formula (engineers × days × hours × productivity) gives you a number, but it misses how that time actually gets used.

### The Five Categories of Work

Every hour your team spends falls into one of these categories:

| Category | Description | Examples |
|---|---|---|
| **Operational** | Keeping systems running | On-call, incidents, deployments, monitoring |
| **Support** | Helping squads use what you've built | PR reviews, questions, pairing, access requests |
| **Planned** | Work you commit to in advance | Platform features, Bicep modules, pipeline templates |
| **Overhead** | Admin and org activities | Meetings, hiring, performance reviews, training |
| **Growth** | Investment in future capability | Learning, certs, innovation spikes, tech radar |

**The problem:** Most managers budget 70-80% of time for Planned work. In reality, for a shared DevOps/Platform team, Planned work typically gets only **40-55%** of available time.

### A Realistic Capacity Breakdown

For a team of **5 engineers** over a **2-week sprint (10 working days)**:

**Gross capacity:** 5 × 10 × 8 hours = 400 hours

**Reality after deductions:**

| Deduction | Percentage | Hours Lost |
|---|---|---|
| Meetings (standups, retros, planning, 1:1s) | 15% | 60 hours |
| On-call rotation overhead | 10% | 40 hours |
| Support & questions from squads | 15% | 60 hours |
| Unplanned interrupts & incidents | 10% | 40 hours |
| Admin, hiring, reviews | 5% | 20 hours |
| **Total deducted** | **55%** | **220 hours** |

**Available for Planned work: ~180 hours (45% of gross)**

This means a 5-person team can realistically commit to roughly **90 story points** (assuming ~2 points/hour), not the 160+ some managers expect.

**Use this as your anchor:** When stakeholders ask "why can't you just add this?", you can show them exactly where the time goes.

### Capacity by Engineer Type

Not all engineers have the same availability:

| Role | Planned Work % | Why Lower |
|---|---|---|
| Senior DevOps Engineer | 40% | More support requests, incident command, code reviews |
| Mid DevOps Engineer | 50% | On-call, support, some mentoring |
| Junior DevOps Engineer | 55% | More learning time, less on-call responsibility |
| Engineering Manager | 20-30% | 1:1s, planning, stakeholder management, hiring |

**Practical tip:** Track actual vs budgeted availability for 2-3 sprints before making capacity commitments. Your real numbers will differ from these estimates.

---

## Work Intake Model for a Shared Team

The biggest mistake shared teams make is **having no single intake process.** Work arrives via Slack DMs, email, verbal requests in standups, tickets raised directly by squads, and "quick questions" that turn into 3-hour investigations.

**The solution: one funnel, one process, regardless of source.**

### The Single Intake Funnel

```
Request arrives (any channel)
        ↓
Logged in intake backlog (within 24 hours)
        ↓
Weekly triage (classified, sized, prioritised)
        ↓
Committed sprint work OR queued with estimated wait
        ↓
Work done → stakeholder notified
```

**Critical rule:** If it's not in the intake backlog, it doesn't exist. This protects your team from invisible work and gives you accurate capacity data.

### Request Classification

Every request gets one of four labels at triage:

| Class | Definition | SLA Commitment |
|---|---|---|
| **Critical** | Production system down, security breach, compliance failure | Respond in <1 hour, work starts immediately |
| **Urgent** | Blocking a squad sprint or release | Triaged within 1 day, start within 2 days |
| **Standard** | Squad request, improvement, new capability | Triaged within 1 week, estimate given within 2 weeks |
| **Platform Initiative** | Proactive platform work from your roadmap | Roadmap-based, communicated quarterly |

### Intake Request Template

Every Standard or Urgent request should fill this in. Incomplete requests go back to the requester before triage.

```markdown
## Request: [Short title]

**Requesting squad/team:** [Squad name and lead]
**Submitted by:** [Name]
**Date submitted:** [Date]

### What are you asking for?
[Describe what you need in plain terms]

### Why do you need it?
[Business context: what problem does this solve, what outcome does it enable]

### Who is affected if this isn't done?
[Team, system, customers, deadline]

### Definition of Done
[How will you know this is complete? What does success look like?]

### Proposed classification:
[ ] Critical - Production impacted
[ ] Urgent - Blocking sprint/release
[ ] Standard - Improvement/new capability

### Dependencies / context
[Anything the platform team needs to know]
```

**Why this matters:** Vague requests waste triage time. This template forces squads to think clearly, and gives your team enough information to estimate and prioritise without a back-and-forth.

### Weekly Triage Cadence

**Meeting:** 45 minutes, weekly (Monday works well)

**Attendees:**
- Platform/DevOps EM (facilitator)
- Senior platform engineer (technical sizing)
- Optional: Rotating squad rep (builds trust, gives context)

**Agenda:**

| Time | Activity |
|---|---|
| 10 min | Review new requests since last triage |
| 15 min | Classify and size each new request |
| 10 min | Update priorities and queue order |
| 10 min | Identify anything that affects current sprint commitments |

**Output:**
- Updated backlog with classifications and rough estimates
- Anything Critical/Urgent flagged for immediate action
- Stakeholders notified of queue position for Standard requests

---

## Capacity Allocation Across Squads

Once you know your true capacity, you need to allocate it intentionally — not reactively.

### The Allocation Model

Think of your team's capacity as a **budget with fixed envelopes**. Before any sprint, the envelopes are filled first:

```
Total Available Capacity (e.g., 180 hours)
│
├── Operational (20%): 36 hours
│   On-call response, deployment support, monitoring
│
├── Unplanned / Urgent Buffer (10%): 18 hours
│   For Critical and Urgent requests that arrive mid-sprint
│
├── Squad Requests (30%): 54 hours
│   Standard requests from squads, distributed by priority
│
└── Platform Roadmap (40%): 72 hours
    Proactive platform work: modules, pipelines, DevEx improvements
```

**The ratios above are starting points, not fixed rules.** Adjust based on your team's reality:
- High-demand period (large release incoming)? Increase Squad Requests to 40%, reduce Roadmap.
- Platform team is new? Invest 50% in Roadmap to build the foundation squads need.
- Operational work keeps expanding? That's a signal — not a budget item to increase, but a problem to solve.

### Distributing Squad Request Capacity Across Teams

When multiple squads want pieces of your 30% (54 hours in the example above), you need a fair allocation method.

**Option A: First-Come, First-Served with Priority Override**
- Requests join a shared queue
- Worked in priority order within the Standard class
- Simple, transparent, slightly frustrating for teams at the back

**Option B: Squad Allocations (Time-Boxing per Squad)**
- Each squad gets a guaranteed slice of your squad request hours per sprint
- Example: 3 squads × 18 hours = 54 hours
- Prevents one loud squad from consuming all shared capacity
- Better for trust; slightly less efficient

**Option C: Rolling Priority (Recommended)**
- No fixed per-squad allocation
- Prioritise by: business impact + strategic alignment + time waiting
- Squads that have waited longest get a bump in priority
- Prevents starvation, rewards patience

**Communicating your allocation:**
Publish your allocation model on your team's wiki or Confluence. Squads should know *how* you prioritise before they raise a request, not after they're frustrated.

```markdown
## How We Allocate Capacity

Each sprint our team has approximately [X hours] of available planned capacity.

We allocate it as follows:
- 40% to Platform Roadmap (proactive improvements for all squads)
- 30% to Squad Requests (triaged by impact and wait time)
- 20% to Operational work (on-call, incidents, deployments)
- 10% buffer for urgent/unplanned items

**What this means for your request:**
Standard requests typically wait 1-3 sprints before starting.
Urgent requests (blocking your sprint) are typically started within 2 days.
Critical requests (production impact) are started within 1 hour.

View our current queue: [link]
```

---

## Queue Management and Wait Time Transparency

The single biggest frustration stakeholders have with shared teams is not knowing **when** their work will be done. "It's in the backlog" is not an answer.

### Maintaining a Visible Queue

Your intake backlog should be **public and always up to date.** Use Jira, Azure DevOps Boards, or even a shared Confluence page — the tool matters less than the visibility.

**Every item in the queue should show:**
- Request title and description
- Requesting squad
- Classification (Critical / Urgent / Standard)
- Date submitted
- Priority order (position in queue)
- Rough size estimate (if triaged)
- Status (Waiting / In Progress / Done)
- Estimated start sprint (if known)

**Board setup example (Azure DevOps / Jira):**

```
Columns:
[Intake] → [Triage] → [Queued] → [In Progress] → [Done]

Labels/Tags:
- Squad-A, Squad-B, Squad-C (for filtering by requester)
- Critical, Urgent, Standard (classification)
- Roadmap, Squad-Request, Operational (work type)
```

### Calculating and Communicating Wait Times

When a squad asks "when will you get to our request?" you need a data-driven answer, not a guess.

**Simple wait time formula:**

```
Estimated Wait = (Items Ahead in Queue × Average Cycle Time) / Sprint Capacity for Standard Requests
```

**Example:**
- 8 Standard requests ahead of Squad C's request
- Average cycle time per request: 6 hours
- Standard request budget per sprint: 54 hours
- Sprints per week: 0.5 (2-week sprints)

```
Weeks to start = (8 × 6) / 54 = 0.88 sprints ≈ 2 weeks
```

Round up and add one sprint buffer for honesty:

> "Based on the current queue, we expect to start your request in approximately **3-4 weeks** (Sprint 14 or 15). We'll confirm at next triage."

**Key phrases that build trust:**
- "Based on the current queue..." (data-driven, not a promise)
- "We'll review at next triage if priorities change" (sets expectation for updates)
- "If this becomes urgent/critical, let us know and we'll reassess" (gives them an option)

### Queue Aging: What to Do With Stale Requests

Every 6-8 weeks, review items that have been waiting more than 3 sprints:

**Options for stale requests:**
1. **Re-prioritise:** Has business context changed? Is it more urgent now?
2. **Deprioritise or close:** If it's been waiting 3 months and nobody has chased it, it probably isn't that important. Close with a message to the requester.
3. **Delegate:** Can the squad do it themselves with guidance? Provide documentation and close.
4. **Escalate:** If it should have been done but keeps getting bumped, raise it to leadership.

**Stale request message to squads:**

> "We noticed [request name] has been in our queue for 10 weeks. Before we reprioritise for next quarter, can you confirm: (a) is this still needed? (b) has urgency changed? (c) can we close this? We'll close it in 5 days if we don't hear back."

### Limiting Work in Progress (WIP)

Context switching is expensive. A DevOps engineer jumping between 5 squad requests helps nobody quickly.

**WIP limits by team size:**

| Team Size | Max Parallel Work Items |
|---|---|
| 2-3 engineers | 2-3 items in progress |
| 4-6 engineers | 4-5 items in progress |
| 7-10 engineers | 6-7 items in progress |

**The rule:** When you hit the WIP limit, **nothing new starts until something finishes.** This feels counterintuitive but dramatically improves throughput and predictability.

---

## SLA/SLO Framework for Shared Teams

An SLA (Service Level Agreement) is a commitment about how you'll respond to and complete work. Publishing clear SLAs shifts the conversation from "why isn't it done?" to "we agreed it would take this long."

### Defining Your SLAs

**Response SLA:** How quickly will you acknowledge the request?
**Start SLA:** How quickly will work begin?
**Completion SLA:** How quickly will it be finished?

Not every class needs all three — Critical needs all three defined, Standard may only commit to response and a rough estimate.

```markdown
## Platform Team SLAs

### Critical (Production Down / Security Breach)
- Response: Within 1 hour (any time, including weekends via on-call)
- Start: Immediately on acknowledgement
- Target completion: Within 4 hours (complex issues may require follow-up)

### Urgent (Blocking Squad Sprint or Release)
- Response: Within 4 business hours
- Start: Within 1 business day
- Target completion: Within 3 business days

### Standard (Squad Request / New Capability)
- Response: Within 1 business day (acknowledged in triage queue)
- Estimate: Within 2 weeks (after triage)
- Start: Based on queue position (communicated at triage)
- Completion: Communicated at sprint planning when item is committed

### Platform Roadmap Initiatives
- Governed by quarterly roadmap process
- Communicated at sprint reviews and stakeholder updates
```

### Publishing and Sticking to SLAs

**Where to publish:** Team wiki, Confluence, or the header of your intake backlog board.

**Sticking to SLAs:**
- Track SLA compliance as a team metric (target: >90% for Critical, >85% for Urgent)
- When you miss an SLA, notify the requester proactively — don't wait for them to chase
- Review SLA breaches in retrospectives (are they preventable?)
- If you're consistently missing SLAs, the problem is the SLA or the capacity — fix one

**SLA breach message:**

> "We committed to starting [request] by [date]. Due to [unexpected incident / team capacity / higher priority item], we haven't been able to start yet. New expected start: [date]. We're sorry for the delay — if this has become blocking, please let us know and we'll reassess urgency."

---

## Stakeholder Communication and Expectation Setting

Running a shared team well is 50% execution, 50% communication. Stakeholders who understand your capacity and process are far more patient than those in the dark.

### The Monthly Capacity Snapshot

Once a month, send a one-page capacity summary to all squad leads and relevant stakeholders.

**Template:**

```markdown
## Platform Team Capacity Update — [Month]

### Current Team Capacity
- Engineers: [X]
- Available hours this month: [Y]
- Planned work capacity: [Z hours (~X%)]

### This Month's Allocation
| Work Type | Hours | % |
|---|---|---|
| Platform Roadmap | [X] | 40% |
| Squad Requests | [X] | 30% |
| Operational | [X] | 20% |
| Buffer | [X] | 10% |

### Active Work This Month
| Item | Squad | Status | Est. Complete |
|---|---|---|---|
| [work item] | [squad] | In Progress | [date] |
| [work item] | [squad] | In Progress | [date] |

### Queue Snapshot
- Items in queue: [X]
- Average wait time for new Standard requests: [Y weeks]
- Oldest unstarted Standard request: [X weeks old]

### Completed Last Month
- [Item 1]
- [Item 2]

### Capacity Concerns / Watch Items
[Any issues: sustained overload, upcoming demand spike, team leave]

Questions? Raise in #platform-team or triage our request form: [link]
```

**Why this works:** Stakeholders get visibility before they have to ask. It also surfaces capacity problems to leadership early, giving you data for headcount conversations.

### Capacity Review Meetings

**Cadence:** Quarterly (aligned with planning cycles)

**Attendees:**
- Platform EM (facilitator)
- Senior platform engineer
- Squad leads or EMs from each team you serve
- Your EM/Director

**Agenda (60 minutes):**

| Time | Topic |
|---|---|
| 10 min | Previous quarter: what we delivered, SLA performance |
| 15 min | Capacity model: team capacity, actual vs planned |
| 20 min | Demand forecast: upcoming requests from squads |
| 10 min | Next quarter allocation and roadmap |
| 5 min | Questions and alignment |

**Key outcome:** Squads leave knowing what to expect next quarter. You leave with any headcount or priority escalations agreed with leadership.

### When Demand Exceeds Supply: Escalation Path

If the queue consistently grows faster than you can work through it, you have a supply/demand imbalance. This is a **business problem**, not a team problem — and needs to be escalated.

**Escalation triggers:**
- Standard request wait time exceeds 8 weeks consistently
- SLA compliance drops below 80% for 2+ months
- Team is consistently working more than 40 hours/week to keep up
- Platform roadmap is being completely displaced by squad requests

**How to escalate:**

1. **Quantify the gap.** "We have 40 hours/sprint of demand for Standard requests but only 24 hours of capacity. The backlog is growing by ~16 hours/sprint."

2. **Show business impact.** "Squad A has been waiting 10 weeks for [infrastructure work] which is blocking their release. Squad C's [security request] has been waiting 8 weeks."

3. **Present options, not just problems:**
   - Option A: Hire 1 additional platform engineer (addresses X months of growth)
   - Option B: Reduce squad request SLA commitments (standard to 6 week wait)
   - Option C: Enable squads to self-serve more (platform investment, 2 sprint upfront cost)
   - Option D: Prioritise ruthlessly — only X squad gets support this quarter

4. **Ask for a decision.** "Which option do you want to pursue? Without a decision, demand will continue to exceed supply and quality and morale will suffer."

---

## Demand Forecasting

Reactive capacity planning is like driving by only looking in the rear-view mirror. Build habits to look ahead.

### Using Historical Data

After 2-3 quarters of consistent intake logging, you'll start to see patterns:

- **Average requests per sprint per squad** (baseline demand)
- **Seasonal spikes** (e.g., pre-release periods, compliance deadlines, new product launches)
- **Growth trend** (is demand growing 10% per quarter? 30%?)

**Simple forecast model:**

```
Next quarter demand = (Average sprint demand) × (sprints in quarter)
                    + (Known spike events × estimated additional demand)
                    + (Demand growth trend × quarters)

Example:
Average demand: 60 hours/sprint
Sprints next quarter: 6
Known spike (major release): +20 hours
Growth trend: +5% per quarter

Forecast = (60 × 6) + 20 + (360 × 0.05)
         = 360 + 20 + 18
         = 398 hours needed

Capacity: 5 engineers × 6 sprints × 36 hours (planned work budget) = ~432 hours

Result: Roughly balanced, but no room for engineer leave or extra incidents.
```

### Leading Indicators of Demand Spikes

Watch for these signals:

| Signal | Likely Impact |
|---|---|
| Large product release scheduled | +30-50% infrastructure requests in the sprint before |
| New squad forming | Onboarding requests for 2-3 sprints |
| Security audit or compliance review | Defender/policy-related requests flood in |
| Organisation restructure | Confusion, access changes, new requirements |
| Major incident | Post-mortem actions create follow-up work |
| End of financial year | Cost reporting, licence reviews |

Build a **demand calendar** — a simple spreadsheet noting known events per quarter. Review it in your quarterly capacity planning meeting.

### Headcount Planning: When to Hire

The question isn't "are we busy?" (you always will be). It's "is the demand permanently above capacity?"

**Hire when:**
- Backlog has grown for 3+ consecutive months (not just a spike)
- SLA compliance is consistently below target despite prioritisation
- Planned roadmap work is zero or near zero (all capacity consumed by reactive work)
- Engineers are consistently working overtime to keep up
- Team morale or attrition is being driven by workload

**Build the business case:**

```markdown
## Headcount Request: 1 Platform Engineer

### Current State
- Team: 5 platform engineers
- Average sprint demand: 400 hours
- Average sprint capacity (planned work): 300 hours
- Persistent backlog growth: +16 hours/sprint for 4 months
- SLA compliance (Urgent): 74% (target: 85%)

### Impact of Status Quo
- [Squad A] release delayed [X weeks] due to infrastructure backlog
- Burnout risk: team is averaging 45-hour weeks for past 6 weeks
- Planned platform roadmap is 0% complete this quarter

### Impact of Additional Hire
- Adds ~60 hours/sprint planned work capacity (+20%)
- Closes current 100-hour deficit within 2 quarters
- Restores SLA compliance to target
- Frees 10-15% of capacity for roadmap work

### Cost vs Benefit
- Cost: [salary + benefits + tooling]
- Benefit: Squads unblocked, platform investment resumes, team sustainable
```

---

## Handling Overload

Despite good planning, overload happens. Know how to recognise it and respond before it causes serious damage.

### Recognising Overload Early

**Team signals:**
- Engineers saying "I'm fine" but working evenings/weekends
- Quality dropping (more incidents, skipped code reviews)
- Retrospective complaints about workload (for multiple sprints)
- Quieter in standups, less initiative
- Attrition risk rising

**Metric signals:**
- Unplanned work % above 35% for 2+ sprints
- SLA compliance trending down
- Planned work completion rate below 60% consistently
- Queue length increasing every sprint

### The Circuit Breaker: Pausing Intake

When overload is severe, temporarily **pause Standard intake.** This is a deliberate tool, not a failure.

**How to communicate the circuit breaker:**

> "Due to a sustained period of high operational demand, the Platform team is pausing new Standard request intake for [2 weeks / this sprint]. We will continue to handle Critical and Urgent requests normally.
>
> We're using this time to work through the existing backlog and recover team capacity. Standard intake will resume on [date].
>
> If you have a request that cannot wait, raise it as Urgent with justification and we'll assess it in triage."

**What to do during the circuit breaker:**
- Clear oldest / highest-priority backlog items
- Let the team work at a sustainable pace
- No new initiatives, no new squad requests
- Use the breathing room to improve a process that's causing recurring work

### Post-Crunch Recovery

After a period of sustained overload (major incident response, pre-release crunch, etc.):

1. **Acknowledge it openly.** "The team carried a heavy load for 6 weeks. That's not sustainable, and it matters."
2. **Reduce planned work for 1 sprint.** Let people breathe. Accept lower throughput.
3. **Protect growth time.** Overloaded teams stop learning. Guarantee a sprint where engineers spend 20% on development.
4. **Review what caused it.** Was this predictable? Could better forecasting have prevented it?

---

## Metrics to Track Capacity Health

You can't manage what you can't measure. Track these every sprint:

| Metric | How to Measure | Target | Warning Sign |
|---|---|---|---|
| **Queue Length** | Count of unstarted items | Stable or shrinking | Growing 3+ sprints |
| **Average Wait Time** | Days from submission to start for Standard | <4 weeks | >8 weeks |
| **SLA Compliance** | % of SLAs met by class | >90% Critical, >85% Urgent | Below target 2+ months |
| **Unplanned Work %** | Unplanned hours / total hours | <25% | >35% |
| **Planned Completion Rate** | Committed items completed / committed | >85% | <70% |
| **Team Utilisation** | Actual planned hours / available hours | 70-75% | >85% sustained |
| **Roadmap Completion** | Platform roadmap items delivered | >50% per quarter | Near 0% |

**Review these in your monthly 1:1s with engineers and in sprint retrospectives.** Don't hide them — showing the data to stakeholders builds trust.

### Capacity Health Dashboard (Simple Version)

A Confluence or SharePoint page updated monthly:

```markdown
## Platform Team Capacity Health — [Month]

| Metric | This Month | Last Month | Target | Status |
|---|---|---|---|---|
| Queue length | 14 | 11 | Stable | ⚠️ Growing |
| Avg wait time (Standard) | 3.5 wks | 2.8 wks | <4 wks | ✅ OK |
| SLA compliance (Urgent) | 88% | 91% | >85% | ✅ OK |
| Unplanned work % | 28% | 22% | <25% | ⚠️ Elevated |
| Planned completion | 81% | 78% | >85% | ⚠️ Below target |
| Team utilisation | 73% | 71% | 70-75% | ✅ Healthy |
| Roadmap progress | 35% | - | >50% | 🔴 Behind |

**Overall status: ⚠️ Watch — elevated unplanned work and queue growth**

**Action:** Investigating source of unplanned work increase. Consider circuit breaker if trend continues next sprint.
```

---

## Practical Templates

### Template 1: Sprint Allocation View

Use this in sprint planning to show where capacity is going:

```markdown
## Sprint [X] Capacity Allocation — Platform Team

**Total Available:** [X] hours

| Work Type | Budget | Items | Hours Committed |
|---|---|---|---|
| Platform Roadmap | 40% ([X] hrs) | [Item A], [Item B] | [X] hrs |
| Squad Requests | 30% ([X] hrs) | [Squad A req], [Squad B req] | [X] hrs |
| Operational | 20% ([X] hrs) | On-call, known deployments | [X] hrs |
| Buffer | 10% ([X] hrs) | (Reserved for urgent/unplanned) | — |

**What we're NOT committing to this sprint:**
- [Item C] — queued for Sprint [Y]
- [Item D] — pending triage

**Communicated to squads:** [date]
```

### Template 2: Monthly Stakeholder Capacity Summary

*(See [Stakeholder Communication](#stakeholder-communication-and-expectation-setting) section above for full template)*

### Template 3: Stakeholder Capacity FAQ

Pin this to your Slack channel or wiki so squads can self-serve answers.

```markdown
## Platform Team — Frequently Asked Questions

**Q: How do I submit a request?**
A: Use the intake form here: [link]. Requests not submitted via form may not be triaged.

**Q: How long will my request take?**
A: Standard requests typically wait 2-4 weeks before starting, depending on queue.
   View the current queue: [link]
   Urgent requests (blocking your sprint): typically started within 1-2 days.

**Q: How is work prioritised?**
A: We prioritise by: class (Critical > Urgent > Standard), then business impact,
   then time waiting. No squad gets automatic priority — it's based on need.

**Q: My request has been waiting 6 weeks. What's happening?**
A: Check the queue for your item's position. If it's been more than 6 weeks without
   movement, DM [EM name] or raise it in #platform-team.

**Q: Can I get something done faster?**
A: Yes — reclassify as Urgent (with justification) and we'll assess it at next triage.
   If it's truly Critical (production impact), contact the on-call engineer directly.

**Q: Why do you have a roadmap? Shouldn't you only do what squads ask for?**
A: Platform investment (our roadmap) directly reduces the support burden and enables
   self-service. Without it, squad wait times would increase. Our roadmap exists to
   make your experience better, not to work on things you don't need.

**Q: I think my request should be higher priority. Who do I talk to?**
A: Raise it in #platform-team or bring it to your squad lead to discuss at
   our monthly capacity review.
```

### Template 4: Quarterly Demand Forecast

```markdown
## Platform Team Demand Forecast — Q[X]

### Capacity Available
- Engineers: [X] (note: [name] on leave weeks [Y-Z])
- Sprints: [X]
- Estimated planned work capacity: [X] hours

### Known Demand
| Source | Estimated Hours | Notes |
|---|---|---|
| Squad A — Release prep | 40 | Major release week [X] |
| Squad B — Onboarding requests | 20 | New engineer joining |
| Compliance audit follow-up | 30 | Defender recommendations |
| Platform roadmap | [X] | See roadmap doc |
| Baseline operational | [X] | Historical average |

### Forecast Summary
| | Hours |
|---|---|
| Total demand forecast | [X] |
| Total capacity | [X] |
| **Balance** | **[+/-X]** |

### Risks
- [Risk 1]: If [event] happens, demand could increase by [X] hours
- [Risk 2]: If [engineer] is pulled for [project], capacity drops by [X] hours

### Recommended Actions
- [Action 1]
- [Action 2]
```

---

## Quick Reference: Capacity Health Checklist

Use monthly to check you're running a healthy shared team:

**Intake & Queue:**
- [ ] All requests logged in intake backlog within 24 hours
- [ ] Weekly triage happening consistently
- [ ] Queue visible and public
- [ ] No request waiting >8 weeks without communication

**Capacity:**
- [ ] Team utilisation between 70-75% (not 90%+)
- [ ] Unplanned work below 25%
- [ ] Planned completion rate above 85%
- [ ] Roadmap getting at least 30% of capacity

**Stakeholder Communication:**
- [ ] Monthly capacity snapshot sent
- [ ] Queue wait times communicated to requesters
- [ ] SLA breaches communicated proactively
- [ ] Capacity review meeting happening quarterly

**Team Health:**
- [ ] No sustained overtime (>40hrs/week for multiple engineers)
- [ ] Growth time protected each sprint
- [ ] Retrospectives include capacity/workload discussion

---

## Related Resources

- [Planning & Prioritization](planning-prioritization.md) - RICE scoring, intake templates, interrupt budgets
- [Stakeholder Management](../leadership/stakeholder-management.md) - Communication, managing up, influence
- [Saying No](../heuristics/saying-no.md) - Scripts for declining or deferring requests
- [On-Call](on-call.md) - On-call rotation scheduling and capacity impact
- [Burnout Prevention](../heuristics/burnout-prevention.md) - Recognising and preventing team burnout
- [Team Health Metrics](team-health-metrics.md) - Measuring team performance
- [DevOps Career Ladder](devops-career-ladder.md) - Level expectations and capacity per role
- [Prompt Bank: Capacity Planning](../prompt-bank/platform-prompts.md#team-capacity-planning)

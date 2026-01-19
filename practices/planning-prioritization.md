# Planning & Prioritization

Managing incoming work, setting priorities, and building sustainable roadmaps.

## The Challenge

**Your team has:**
- Finite capacity
- Infinite demands
- Competing priorities
- Urgent requests
- Technical debt
- Strategic initiatives
- Bugs and maintenance

**You need to:**
- Deliver business value
- Keep systems healthy
- Develop your team
- Satisfy stakeholders
- Stay sane

**Everything can't be a priority.**

## Prioritization Frameworks

### 1. RICE Score

**Components:**
- **Reach:** How many people affected?
- **Impact:** How much does it help? (Massive=3, High=2, Medium=1, Low=0.5, Minimal=0.25)
- **Confidence:** How sure are we? (High=100%, Medium=80%, Low=50%)
- **Effort:** How much work? (person-months)

**Formula:**
```
RICE Score = (Reach × Impact × Confidence) / Effort
```

**Example:**
- Reach: 10,000 users
- Impact: High (2)
- Confidence: 80%
- Effort: 2 person-months

Score = (10,000 × 2 × 0.8) / 2 = 8,000

**Higher score = higher priority**

### 2. Value vs Effort Matrix

```
        High Value
             ↑
    Quick   |  Major
    Wins    |  Projects
    DO      |  PLAN
←───────────┼───────────→
    Fill-   |  Money
    Ins     |  Pits
    LAST    |  AVOID
             ↓
        Low Value
```

**Quick Wins:** High value, low effort - do these first
**Major Projects:** High value, high effort - plan and schedule
**Fill-Ins:** Low value, low effort - do when spare time
**Money Pits:** Low value, high effort - avoid or kill

### 3. ICE Score (Simplified RICE)

**Simpler version:**
- **Impact:** Business impact (1-10)
- **Confidence:** How sure? (1-10)
- **Ease:** How easy? (1-10)

**Formula:**
```
ICE Score = (Impact × Confidence × Ease) / 3
```

**Use when:** Don't have precise reach/effort data

### 4. Weighted Scoring

**Define criteria with weights:**
- Customer value (30%)
- Revenue impact (25%)
- Strategic alignment (20%)
- Technical feasibility (15%)
- Time to market (10%)

**Score each item 1-10 on each criterion, multiply by weight, sum**

**Example:**
- Customer value: 8 × 0.30 = 2.4
- Revenue: 6 × 0.25 = 1.5
- Strategic: 9 × 0.20 = 1.8
- Feasibility: 7 × 0.15 = 1.05
- Time: 5 × 0.10 = 0.5
- **Total: 7.25**

### 5. Kano Model

**Categorize features:**

**Basic Needs (Must-Haves):**
- Customers expect these
- Dissatisfied if missing
- Not delighted when present
- Example: Security, uptime

**Performance Needs (Linear):**
- More is better
- Satisfaction increases linearly
- Example: Speed, cost

**Excitement Needs (Delighters):**
- Unexpected features
- High satisfaction when present
- Not missed if absent
- Example: Innovative features

**Priority:** Basic > Performance > Excitement

### 6. Cost of Delay

**What does waiting cost?**

Calculate: "If we delay this 1 month, what's the impact?"
- Lost revenue
- Customer churn
- Competitive disadvantage
- Regulatory risk

**Higher cost of delay = higher priority**

**CD3 (Cost of Delay Divided by Duration):**
```
CD3 = Cost of Delay / Duration
```

Prioritize highest CD3 first.

## Building a Roadmap

### Roadmap Horizons

**Now (Current Quarter):**
- Committed work
- High confidence
- Specific features

**Next (Next Quarter):**
- Planned work
- Medium confidence
- Themes and epics

**Later (Beyond 2 quarters):**
- Strategic direction
- Low confidence on specifics
- Vision and bets

**Don't over-commit to "Later"** - things change

### Roadmap Components

**Strategic Initiatives (40-50%):**
- Big bets
- New capabilities
- Competitive advantages
- Planned and scheduled

**Technical Debt (20-30%):**
- Refactoring
- Infrastructure improvements
- Performance optimization
- Ongoing maintenance

**Bugs and Support (10-20%):**
- Bug fixes
- Customer support issues
- Small improvements
- Reactive work

**Innovation/Exploration (10-20%):**
- Experiments
- Learning new tech
- Proof of concepts
- Future investments

**Adjust percentages to your context**

### Quarterly Planning

**6-8 weeks before quarter:**
1. Review company/org strategy
2. Gather stakeholder input
3. Assess team capacity
4. Draft roadmap options
5. Review with stakeholders
6. Finalize and commit

**Inputs:**
- Company OKRs/goals
- Customer feedback
- Technical debt backlog
- Team capacity
- Market changes
- Stakeholder requests

**Output:**
- Committed work for quarter
- Success metrics
- Dependencies identified
- Risk assessment

### Theme-Based Roadmaps

**Instead of features, organize by themes:**

**Q1 Theme: "Performance"**
- API response time improvements
- Database optimization
- Caching layer
- Monitoring enhancements

**Q2 Theme: "Developer Experience"**
- Better testing tools
- Improved CI/CD
- Documentation
- Local development setup

**Benefits:**
- Flexibility on specific features
- Clear focus
- Easier to communicate
- Outcome-oriented

## Managing Incoming Requests

### Request Intake Process

**1. Capture Everything**
- Single place (ticket system, form, etc.)
- No work without a ticket
- No hallway commitments

**2. Triage Regularly**
- Weekly review
- Categorize and prioritize
- Provide initial estimate
- Set expectations

**3. Backlog Grooming**
- Bi-weekly review
- Remove stale items
- Re-prioritize
- Update estimates

**4. Commitment**
- Work pulled into sprint/quarter
- Only then is it "committed"
- Manage expectations until then

### The Intake Template

```markdown
# Request: [Title]

**Requester:** [Name]
**Date:** [Date]
**Priority:** [Suggested priority]

## What is needed?
[Clear description]

## Why is this needed?
[Business justification]

## Who is impacted?
[Users, teams, customers]

## What happens if we don't do this?
[Cost of not doing]

## When is it needed by?
[Deadline and flexibility]

## Initial Assessment:
- Estimated effort: [S/M/L/XL]
- Priority: [P0/P1/P2/P3]
- Next steps: [Evaluate / Plan / Schedule / Decline]
```

### Saying No to Requests

**You will get more requests than capacity. Must say no.**

**Scripts:**

**Not aligned with strategy:**
"This doesn't align with our Q3 focus on [theme]. Can we revisit in Q4 planning?"

**Capacity constrained:**
"We're at capacity. To take this on, what should we deprioritize from [current roadmap]?"

**Need more info:**
"Before committing, I need to understand [X, Y, Z]. Can we schedule time to discuss?"

**Not the right team:**
"This seems better suited for [other team]. Can I connect you with them?"

**See [Saying No Gracefully](../heuristics/saying-no.md) for more**

## Sprint Planning

### Before the Meeting

**Manager's prep:**
- Review roadmap
- Check team capacity (PTO, meetings, etc.)
- Identify dependencies
- Prepare backlog
- Talk to stakeholders

**Team's prep:**
- Review upcoming work
- Identify blockers
- Technical investigation done
- Questions ready

### During Sprint Planning (2 hours)

**Part 1: What (1 hour)**
- Review sprint goal
- Walk through prioritized backlog
- Discuss each item
- Team asks questions
- Collectively commit to sprint

**Part 2: How (1 hour)**
- Break down larger items
- Identify tasks
- Technical approach discussion
- Dependency mapping
- Final capacity check

**Output:**
- Sprint goal (1-2 sentences)
- Committed work
- Sprint backlog
- Initial task breakdown

### Capacity Planning

**Available hours formula:**
```
Team size × Work days × Hours per day × Productivity factor
```

**Example:**
- 5 engineers
- 10 work days
- 6 productive hours/day (meetings, etc.)
- 0.7 factor (only 70% on sprint work)
- = 5 × 10 × 6 × 0.7 = 210 hours

**Buffer for:**
- Meetings (15-20%)
- Code reviews (10%)
- Helping others (10%)
- Unexpected issues (10%)

**Better to under-commit and over-deliver**

## Handling Interruptions

### The Interrupt Budget

**Reserve capacity for interruptions:**
- Production issues
- Urgent bugs
- Customer escalations
- Team helping each other

**Common allocation: 20-30% of capacity**

**Track actual interrupts:**
- Are we within budget?
- Need to reserve more?
- Can we reduce interruptions?

### Interrupt Classification

**Level 1 - Critical (Drop everything):**
- Production outage
- Security breach
- Data loss
- Do immediately

**Level 2 - Urgent (Same day):**
- Severe bug
- Customer escalation
- Blocking another team
- Fit in today

**Level 3 - Important (This sprint):**
- Significant bugs
- Important requests
- Add to sprint backlog

**Level 4 - Normal (Next sprint):**
- Regular requests
- Minor improvements
- Goes in backlog

**Clearly define levels with stakeholders**

### Emergency Process

**When critical issue arises:**

1. **Assess impact**
   - Who's affected?
   - How severe?
   - Can it wait?

2. **Decide quickly**
   - Pull team from sprint work?
   - Assign specific person?
   - Escalate?

3. **Communicate**
   - Team knows
   - Stakeholders notified
   - Expectations adjusted

4. **Resolve & learn**
   - Fix the issue
   - Post-mortem
   - Prevent recurrence

## Dealing with Competing Priorities

### When Stakeholders Conflict

**Example:**
- Product wants Feature A
- Sales wants Feature B
- Support wants Bug fixes
- CTO wants Tech debt

**Your role: Facilitate decision, not make it**

**Process:**

1. **Gather all requests**
   - Document each with justification
   - Estimated effort
   - Business impact

2. **Make trade-offs visible**
   - "We can do A or B, not both"
   - Show the opportunity cost
   - Use prioritization framework

3. **Facilitate stakeholder alignment**
   - Meeting with decision makers
   - Present options and trade-offs
   - Get single prioritized list
   - Document decisions

4. **Execute and communicate**
   - Build what was agreed
   - Keep stakeholders informed
   - Revisit quarterly

**Document the decision:** Prevents relitigating later

### The Priority Conversation

**Template:**

"We have capacity for X amount of work this quarter. Here are the requests we've received:

A: [Impact, Effort, Requester]
B: [Impact, Effort, Requester]
C: [Impact, Effort, Requester]
D: [Impact, Effort, Requester]

Using [framework], here's the recommended priority:
1. A
2. C
3. B

We can't fit D this quarter.

Does this align with business priorities? What would you change?"

## Managing Technical Debt

### Technical Debt as Portfolio

**Don't ask "Should we do tech debt?"**

**Ask "How much should we invest?"**

**Typical allocation: 20-30% of capacity**

### Prioritizing Tech Debt

**High priority debt:**
- Slowing down feature development
- Causing production issues
- Security risks
- Recruiting/retention impact

**Lower priority debt:**
- Annoying but not blocking
- Old code that doesn't change
- "Nice to have" refactors

**Track:**
- Impact on velocity
- Developer satisfaction
- Production incidents
- Time to onboard new engineers

### Making the Business Case

**Frame in business terms:**

❌ "The code is messy"
✓ "This refactor will reduce bug rate by 30% and speed up feature development by 20%"

❌ "We should rewrite this"
✓ "Current architecture limits us to 1 new feature per sprint. After refactor: 3 features per sprint"

**Show the ROI:**
- Time saved
- Velocity increase
- Incident reduction
- Onboarding speed

## Communicating the Plan

### Roadmap Formats

**For Executives:**
- High-level themes
- Business outcomes
- Metrics and goals
- Quarterly view
- One page

**For Product/Stakeholders:**
- Features and epics
- Release timeline
- Dependencies
- Risks
- Monthly updates

**For Team:**
- Detailed backlog
- Sprint by sprint
- Technical details
- Task breakdown
- Weekly updates

### Setting Expectations

**Be clear about:**
- What's committed vs aspirational
- Confidence levels
- Dependencies and risks
- When decisions will be made
- How to request changes

**Communicate regularly:**
- Weekly: Team updates
- Bi-weekly: Stakeholder sync
- Monthly: Written roadmap update
- Quarterly: Planning and retrospective

### Managing Scope Changes

**When priorities change mid-quarter:**

**Small change:**
- Swap similar-sized items
- Document the trade-off
- Inform affected stakeholders

**Large change:**
- Call it out explicitly
- Re-plan the quarter
- Reset expectations
- Get stakeholder buy-in

**Don't:**
- Silently drop committed work
- Say yes without removing something
- Overwork the team to fit it all

## Metrics for Planning

### Track Over Time

**Velocity:**
- Story points or tickets completed per sprint
- Use for capacity planning
- Not for team comparison

**Throughput:**
- Number of features shipped per quarter
- Trending up or down?
- Why?

**Cycle Time:**
- Idea to production
- Getting faster or slower?
- Where are bottlenecks?

**Plan vs Actual:**
- Did we deliver what we planned?
- What caused variance?
- Improve estimation

### Improvement Indicators

**Good signs:**
- Predictable velocity
- Hitting commitments
- Stakeholder satisfaction
- Team confidence in plans

**Warning signs:**
- Wildly variable velocity
- Constantly missing commitments
- Stakeholder complaints
- Team demoralized

## Common Planning Mistakes

### ❌ Planning Too Far Out

**Problem:** Plans beyond 2 quarters are guesses

**Fix:** Focus on now and next, vision for later

### ❌ Over-Committing

**Problem:** Say yes to everything, deliver little

**Fix:** Be realistic about capacity, buffer for unknown

### ❌ Ignoring Tech Debt

**Problem:** Velocity decreases over time

**Fix:** Dedicate % of capacity to technical health

### ❌ No Stakeholder Alignment

**Problem:** Conflicting priorities, constant changes

**Fix:** Regular stakeholder sync, clear decision process

### ❌ Feature Factory

**Problem:** Just shipping features, no impact measurement

**Fix:** Define success metrics, measure outcomes

### ❌ Bottom-Up Only

**Problem:** No strategic direction, reactive

**Fix:** Balance top-down strategy with bottom-up input

### ❌ Top-Down Only

**Problem:** Unrealistic plans, team not bought in

**Fix:** Involve team in planning, trust their estimates

## Templates

### Quarterly Planning Template

```markdown
# Q[X] YYYY Engineering Plan

## Team: [Team Name]

## Strategic Context
- Company goals for quarter
- Team mission alignment
- Key metrics to move

## Capacity
- Team size: [X] engineers
- Planned PTO: [Y] days
- Available capacity: [Z] story points / [W] person-weeks

## Priorities

### Theme 1: [Name] (40% of capacity)
**Goal:** [Outcome]
**Why:** [Business justification]
**Success Metrics:** [How we'll measure]

Projects:
- [ ] Project A - [Owner] - [Effort]
- [ ] Project B - [Owner] - [Effort]

### Theme 2: Technical Health (25% of capacity)
- [ ] Tech debt item 1
- [ ] Performance improvement 2
- [ ] Infrastructure upgrade 3

### Theme 3: Bugs/Maintenance (15% of capacity)
### Theme 4: Innovation (20% of capacity)

## Risks & Dependencies
- [Risk 1]: [Mitigation]
- [Dependency]: [Owner and status]

## Deferred to Next Quarter
- [Item]: [Why deferred]

## Success Criteria
- [ ] [Metric] reaches [target]
- [ ] [Feature] shipped to [% users]
- [ ] [Technical goal] achieved
```

### Weekly Planning Template

```markdown
# Week of [Date]

## Last Week
✅ Completed:
- [Item]
⚠️ In Progress:
- [Item]
❌ Blocked:
- [Item] - [Blocker]

## This Week Priorities
1. [P0 item]
2. [P0 item]
3. [P1 item]

## Team Capacity
- [Name]: 80% (out Friday)
- [Name]: 100%
- [Name]: 50% (on-call + interviews)

## Risks
- [Risk]: [Plan]

## Help Needed
- [What you need from whom]
```

## Tools

**Roadmap Tools:**
- ProductBoard
- Aha!
- Jira Roadmaps
- Notion
- Google Sheets (simple works!)

**Prioritization:**
- RICE calculator spreadsheet
- Weighted scoring template
- Voting tools (dot voting in Miro)

**Capacity Planning:**
- Jira capacity planning
- Forecast / Monte Carlo tools
- Simple spreadsheets

**Don't over-tool - start simple, add complexity only if needed**

## Resources

- [ ] "Inspired" by Marty Cagan (Product management)
- [ ] "Measure What Matters" by John Doerr (OKRs)
- [ ] "The Goal" by Eliyahu Goldratt (Theory of Constraints)
- [ ] "Making Work Visible" by Dominica DeGrandis
- [ ] "Continuous Discovery Habits" by Teresa Torres

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

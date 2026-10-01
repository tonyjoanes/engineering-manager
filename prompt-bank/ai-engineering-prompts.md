# AI Engineering & Productivity Metrics Prompts

Ready-to-use prompts for leading AI-assisted teams and measuring engineering productivity with current DORA, DevEx and DX Core 4 practice.

---

## AI Readiness Assessment

**When to Use:** Before (or early in) rolling out AI coding assistants or agents, to see whether your team's foundations will let AI help rather than hurt.

**Related Resources:**
- [AI-Assisted Engineering](../practices/ai-assisted-engineering.md#the-dora-ai-capabilities-model)
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)

**The Prompt:**
```
I want to assess how ready [team name] is to get real value from AI coding tools and agents.

Current state against the DORA AI Capabilities Model:
1. AI stance / policy: [do we have one? is it understood?]
2. Data ecosystem quality: [state of docs, data, internal knowledge]
3. AI access to internal context: [do tools know our codebase, docs, tickets? context files? MCP?]
4. Version control practices: [commit frequency, branching, ease of rollback]
5. Batch size: [typical PR size, deploy size]
6. User-centric focus: [how well the team connects work to user outcomes]
7. Internal platform quality: [CI speed, golden paths, self-service]

Current delivery metrics: [change lead time, deployment frequency, change fail rate, rework rate]
Current AI usage: [tools, how widely used, what for]

Help me:
1. Rate each capability (strong / adequate / weak) with reasoning
2. Identify the 2-3 gaps most likely to turn AI speed into rework
3. Recommend a sequenced plan to close them
4. Suggest which AI use cases to start with given our current strengths

Reference the AI-assisted engineering guide for the capabilities model and rollout phases.
```

**Expected Output:**
- Capability scorecard
- Prioritised gaps with rationale
- Sequenced improvement plan
- Recommended starting use cases

**Follow-Up Actions:**
- Share scorecard with team and discuss
- Add top gaps to platform / team roadmap
- Capture baseline metrics before rollout

---

## Team AI Working Agreement

**When to Use:** Creating or refreshing your team's AI usage policy.

**Related Resources:**
- [AI-Assisted Engineering: Setting Your Team's AI Stance](../practices/ai-assisted-engineering.md#setting-your-teams-ai-stance)

**The Prompt:**
```
Help me draft an AI working agreement for [team name].

Context:
- Team: [size, seniority mix, domain]
- Company AI policy: [summary, or "none yet"]
- Approved tools: [list]
- Sensitive data we handle: [customer data, PII, secrets, regulated data]
- Where we already use AI: [current usage]
- Concerns raised by the team: [quality, security, skills, job worries]
- Infrastructure we manage: [e.g. Azure, Bicep, pipelines]

Create a one-page agreement covering:
1. Approved tools and accounts
2. Data rules (what never goes into AI tools)
3. Ownership and review expectations for AI-generated code
4. Where agents can be used freely vs carefully
5. Expectations for junior engineers' learning
6. How we'll share techniques and review this agreement

Keep it short and practical. Reference the AI-assisted engineering guide template.
```

**Expected Output:**
- Draft working agreement ready for team discussion

**Follow-Up Actions:**
- Review together with the team (don't impose it)
- Publish in team wiki / repo
- Add a context file (CLAUDE.md / AGENTS.md) to key repos
- Revisit quarterly

---

## AI Review Load Problem

**When to Use:** Senior engineers are overwhelmed reviewing AI-generated PRs, PRs are getting bigger, or quality is slipping.

**Related Resources:**
- [AI-Assisted Engineering: Managing Review Load](../practices/ai-assisted-engineering.md#managing-review-load)
- [Developer Productivity Metrics](../practices/developer-productivity-metrics.md)

**The Prompt:**
```
Since adopting AI coding tools, code review has become a bottleneck on [team name].

Data:
- Average PR size: [before vs now]
- PRs per week: [before vs now]
- Review wait time: [before vs now]
- Who does most reviews: [distribution]
- Change fail rate / rework rate: [before vs now]
- What reviewers are saying: [quotes]

Help me:
1. Diagnose what's driving the review load
2. Recommend changes to author responsibilities and PR norms
3. Suggest what to automate (AI review, CI gates) vs keep human
4. Spread review load fairly while growing less-senior reviewers
5. Define metrics to know if it's working

Reference the AI-assisted engineering guide for review practices.
```

**Expected Output:**
- Root cause of review overload
- Updated PR / review norms
- Automation recommendations
- Metrics to track

**Follow-Up Actions:**
- Discuss in retro and agree new norms
- Configure AI review / CI gates
- Track PR size and review time for 4-6 weeks

---

## Measuring AI Impact for Leadership

**When to Use:** Leadership asks "what are we getting from our AI investment?"

**Related Resources:**
- [AI-Assisted Engineering: Measuring AI Impact Honestly](../practices/ai-assisted-engineering.md#measuring-ai-impact-honestly)
- [Developer Productivity Metrics](../practices/developer-productivity-metrics.md)
- [Stakeholder Management](../leadership/stakeholder-management.md)

**The Prompt:**
```
I need to report on the impact of AI tools on [team / org] to [audience, e.g. CTO, exec team].

Data available:
- Rollout timeline: [when, which tools, which teams]
- DORA throughput before/after: [change lead time, deployment frequency, recovery time]
- DORA instability before/after: [change fail rate, rework rate]
- PR size and review time trend: [data]
- Developer survey results: [satisfaction, friction, trust in AI]
- % time on new capabilities vs maintenance: [if known]
- Costs: [licences, platform work]
- Anecdotes: [specific wins or problems]

Help me:
1. Build an honest narrative: what improved, what didn't, and why
2. Avoid vanity metrics (% code by AI, lines of code)
3. Identify where the bottleneck has moved
4. Frame next investment asks (platform, testing, review capacity)
5. Structure a one-page summary in business terms

Reference the AI-assisted engineering and developer productivity metrics guides.
```

**Expected Output:**
- One-page impact summary
- Clear statement of current bottleneck
- Investment recommendations

**Follow-Up Actions:**
- Pre-wire key stakeholders
- Agree metrics for next review
- Set up regular (quarterly) reporting

---

## Engineer Over-Relying on AI

**When to Use:** An engineer is shipping AI-generated code they don't understand, review quality is dropping, or they struggle to debug their own changes.

**Related Resources:**
- [AI-Assisted Engineering: Protecting Skill Development](../practices/ai-assisted-engineering.md#protecting-skill-development)
- [Feedback Models](../leadership/feedback-models.md)
- [Difficult Conversations](../leadership/difficult-conversations.md)

**The Prompt:**
```
I need to talk to [engineer name, level] about how they use AI tools.

What I've observed:
- [Specific example 1, e.g. "couldn't explain the approach in PR #123 when asked in review"]
- [Specific example 2, e.g. "two production bugs from untested agent changes"]
- [Specific example 3]

Context:
- Their experience: [level, time on team]
- Strengths: [list]
- Team AI working agreement: [summary]

Help me:
1. Frame the feedback using SBI, focused on outcomes not tool usage
2. Plan questions to understand their perspective
3. Agree specific practices (explain-back, deliberate practice, testing)
4. Set up support (pairing, debugging rotations)
5. Define how we'll know it's improving

Reference the AI-assisted engineering guide and feedback models.
```

**Expected Output:**
- Conversation plan with SBI feedback
- Agreed practices and support
- Follow-up checkpoints

**Follow-Up Actions:**
- Document agreements
- Arrange pairing / mentoring
- Check in at next 1:1s

---

## Background Agent Pilot

**When to Use:** Deciding whether and how to let agents open PRs autonomously (dependency upgrades, test gaps, migrations, etc.).

**Related Resources:**
- [AI-Assisted Engineering: Rolling Out AI Agents](../practices/ai-assisted-engineering.md#rolling-out-ai-agents-a-phased-approach)
- [AI-Assisted Engineering: Security & Risk](../practices/ai-assisted-engineering.md#security--risk)

**The Prompt:**
```
I'm considering a pilot of background coding agents for [use case, e.g. "dependency upgrades across 40 repos"].

Context:
- Repos in scope: [number, languages, IaC]
- Test coverage / CI confidence: [state]
- Current toil: [hours per month, who does it]
- Tooling options: [agents / platforms being considered]
- Security constraints: [secrets, production access, compliance]
- Review capacity: [who will review agent PRs]

Help me:
1. Assess if this use case is a good fit (bounded, verifiable, low risk)
2. Design guardrails (permissions, sandboxing, approval gates, audit)
3. Define success metrics (toil saved, merge rate, rework introduced)
4. Plan the pilot scope, timeline and exit criteria
5. Identify risks, including prompt injection and supply-chain issues

Reference the AI-assisted engineering guide for rollout phases and security mitigations.
```

**Expected Output:**
- Fit assessment
- Guardrail design
- Pilot plan with success / exit criteria

**Follow-Up Actions:**
- Security review of agent permissions and integrations
- Run pilot on a small set of repos
- Review results before scaling

---

## DORA Team Profile Diagnosis

**When to Use:** You want a holistic view of team health and delivery using the DORA 2025 team profiles.

**Related Resources:**
- [Developer Productivity Metrics: Seven Team Profiles](../practices/developer-productivity-metrics.md#dora-2025-seven-team-profiles)
- [Team Health Metrics](../practices/team-health-metrics.md)
- [Retrospectives](../practices/retrospectives.md)

**The Prompt:**
```
Help me work out which DORA 2025 team profile best describes [team name], and what to do about it.

Delivery data:
- Change lead time: [value]
- Deployment frequency: [value]
- Failed deployment recovery time: [value]
- Change fail rate: [value]
- Rework rate: [value]

Human factors:
- Burnout / well-being signals: [survey, observations]
- Friction: [process, approvals, meetings, tooling]
- Product impact: [are we delivering outcomes users value?]
- Reliance on individual heroics: [yes/no, examples]

Help me:
1. Identify the closest profile(s) and explain why
2. Highlight where data and team perception may differ
3. Recommend the 1-2 highest-leverage improvements
4. Design a retro or team session to discuss this with the team

Reference the developer productivity metrics guide for profile descriptions.
```

**Expected Output:**
- Likely profile with reasoning
- Focus areas
- Team session plan

**Follow-Up Actions:**
- Run the session with the team
- Agree improvements and track in retros
- Revisit quarterly

---

## Productivity Measurement Programme

**When to Use:** Setting up (or fixing) how your team or org measures engineering productivity.

**Related Resources:**
- [Developer Productivity Metrics](../practices/developer-productivity-metrics.md#setting-up-a-measurement-programme)

**The Prompt:**
```
I want to set up a productivity measurement approach for [team / org, size].

Context:
- Why now: [leadership ask, AI ROI, platform investment, team health concerns]
- Current metrics: [what we track today, if anything]
- Tooling: [Azure DevOps / GitHub / Jira / incident tool / survey tool]
- Audience: [team, my manager, CTO, finance]
- Concerns: [team worried about being measured, gaming, etc.]

Help me:
1. Pick a framework mix (DORA, DevEx, SPACE, DX Core 4) for our questions
2. Define each metric and how to collect it from our tools
3. Design a short developer survey
4. Plan how to introduce it without damaging trust
5. Set the reporting cadence for team vs leadership

Reference the developer productivity metrics guide.
```

**Expected Output:**
- Metric set with definitions and data sources
- Survey draft
- Rollout and communication plan

**Follow-Up Actions:**
- Agree definitions with the team
- Baseline for 2-4 weeks
- Share results with the team first

---

## Related Prompt Banks

- [Platform Prompts](platform-prompts.md) - Platform and DevOps topics
- [Team Prompts](team-prompts.md) - Team health and dynamics
- [Leadership Prompts](leadership-prompts.md) - Feedback, performance, coaching
- [Strategic Prompts](strategic-prompts.md) - Planning and stakeholder management

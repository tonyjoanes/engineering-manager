# AI-Assisted Engineering

Leading a team where AI coding assistants and agents are part of everyday work: what changes, what doesn't, and how to manage it well.

## Why This Matters

AI tools are now standard. The 2025 DORA report ("State of AI-assisted Software Development") found roughly **90% of technology professionals use AI at work**, yet a large minority report **little or no trust** in the code it produces.

**The headline finding from DORA 2025:**

> AI doesn't fix a team; it **amplifies** what's already there.

- Strong teams (good platforms, small batches, clear ownership) get faster *and* stay stable
- Struggling teams get more code, more review load, more instability - and their existing problems get louder

**Implication for managers:** your job isn't to "roll out AI". It's to make sure the system around the AI - platform, workflow, review, quality gates, skills - is healthy enough that AI acceleration lands as value rather than as rework.

## What Actually Changes

### The bottleneck moves

```
Before AI:  Writing code ──► (bottleneck)
With AI:    Writing code ──► Reviewing ──► Testing ──► Deploying ──► Operating
                              (new bottleneck moves downstream)
```

**Writing code gets cheaper. Everything else stays the same cost or gets more expensive:**
- Code review volume goes up (more PRs, bigger PRs)
- Understanding code you didn't write takes longer
- Integration and test pipelines get busier
- Production incidents from plausible-but-wrong code

**If your delivery pipeline was already slow, AI makes the queue longer, not shorter.** This is why DORA's capabilities (below) are mostly *not* about AI.

### Work types shift

| Work | Impact of AI | Manager focus |
|------|--------------|---------------|
| Boilerplate, scaffolding, tests | Large speed-up | Make sure tests are meaningful, not just present |
| Migrations, upgrades, refactors | Large speed-up with agents | Good place to start agentic work - clear, verifiable goals |
| Debugging unfamiliar code | Moderate speed-up | Pair AI explanation with human verification |
| Novel design / architecture | Small speed-up, useful as a sounding board | Keep humans accountable for decisions (ADRs) |
| Understanding the business problem | Little change | Still the core engineering skill |
| Code review | Load **increases** | Biggest new constraint - plan for it |

### The tool landscape (2026)

Three broad modes - most teams use all three:

**1. Inline assistance** - autocomplete and chat in the IDE (GitHub Copilot, Cursor, JetBrains AI, etc.)
- Low risk, small units of change, engineer stays in control

**2. Interactive agents** - engineer directs an agent that reads the repo, edits multiple files, runs tests and commands (Claude Code, Copilot agent mode, Cursor agent, Codex, etc.)
- Large units of change, engineer reviews the result
- Quality depends heavily on repo context and test suite

**3. Background / autonomous agents** - agents pick up an issue and open a PR without a human in the loop until review (cloud agents, CI-triggered agents, AI code review bots)
- Highest leverage, highest need for guardrails
- Treat agent PRs like PRs from a new contractor: same bar, same review

**Supporting infrastructure:**
- **Repo context files** (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`) - tell agents how to build, test and follow conventions
- **MCP (Model Context Protocol) servers** - give agents controlled access to internal systems (tickets, docs, observability, cloud resources)
- **AI code review** - first-pass review bots that catch issues before a human looks

## The DORA AI Capabilities Model

DORA 2025 identified **seven capabilities** that amplify the benefit of AI adoption. Use them as your AI readiness checklist:

| # | Capability | What it means | Manager question |
|---|-----------|---------------|------------------|
| 1 | **Clear and communicated AI stance** | People know which tools are allowed, for what, and with what data | "Could any engineer tell me our AI policy in two sentences?" |
| 2 | **Healthy data ecosystems** | Internal data is high quality, accessible and unified | "Is our documentation / data good enough to be useful to a model?" |
| 3 | **AI-accessible internal data** | AI tools can reach internal context (code, docs, tickets) safely | "Do our tools know about our codebase and conventions, or just the internet?" |
| 4 | **Strong version control practices** | Frequent commits, easy rollback, everything in VCS | "If an agent makes a mess, how fast can we undo it?" |
| 5 | **Working in small batches** | Small PRs, small deploys, fast feedback | "Is AI making our PRs bigger?" |
| 6 | **User-centric focus** | Teams anchored on user outcomes, not output | "Are we shipping more *value*, or just more *code*?" |
| 7 | **Quality internal platforms** | Golden paths, self-service, fast reliable pipelines | "Can our pipeline absorb 2x the PR volume?" |

**Notice:** five of the seven are just good engineering. Investment in your [platform](./platform-engineering-devex.md) and delivery practices *is* AI investment.

**Key finding:** without capability #6 (user-centric focus), DORA found AI adoption can actually *hurt* team performance - teams get busier without getting better.

## Setting Your Team's AI Stance

Write it down. One page. Revisit quarterly - tools change fast.

### Template

```markdown
# Team AI Working Agreement

## Approved tools
- [Tool] for [use], via [company account/licence]
- Personal accounts / unapproved tools: not for company code or data

## Data rules
- Never paste: secrets, credentials, customer data, PII, [other]
- Allowed context: our repos, internal docs, [other]
- MCP servers / integrations: only from the approved list

## Ownership
- You own every line you merge, however it was written
- "The AI wrote it" is never an explanation in a review or post-mortem

## Review
- AI-generated PRs meet the same bar as any other PR
- Author must have read and understood every change before requesting review
- Keep PRs small - split agent output if needed
- Label agent-authored PRs [if useful for your metrics]

## Where we use agents freely
- Tests, migrations, dependency upgrades, docs, scripts, prototypes

## Where we're careful
- Security-sensitive code (auth, crypto, permissions)
- Infrastructure changes to production (Bicep/Terraform plans reviewed by a human)
- Anything we can't easily verify with tests

## Learning
- Juniors: [expectations - see "Protecting skill development"]
- Share prompts, context files and techniques in [channel / show-and-tell]
```

### Repo context files

The single highest-leverage, lowest-cost practice. Every repo should have a context file that tells agents (and new humans):
- How to build, test and lint
- Architecture overview and key directories
- Conventions (naming, error handling, patterns to use / avoid)
- What not to touch

**Treat it like onboarding docs:** if an agent keeps making the same mistake, the fix is usually a line in the context file. Review changes to it like code.

## Managing Review Load

The most common failure mode: a few senior engineers drown in AI-generated PRs.

### Warning signs
- PR size trending up
- Review wait time trending up
- Seniors reviewing all day, not designing or coding
- Approvals getting faster but change fail rate rising ("rubber-stamping")
- Reviewers can't tell if the author understands the change

### Practices that help

**1. Author responsibility first**
- The author reviews their own (AI) diff before anyone else sees it
- PR description explains *why* and *how it was verified*, not just *what*
- Author can answer "why this approach?" without re-asking the AI

**2. Keep batches small**
- Agents happily produce 2,000-line PRs. Don't accept them.
- Split by concern: refactor PR, then behaviour PR
- Stacked PRs for larger agent work

**3. Automate the first pass**
- AI review bots for style, obvious bugs, missing tests
- Strong CI: lint, types, tests, security scanning
- Humans focus on design, correctness, and "should we do this at all?"

**4. Spread review across the team**
- Review rotation, not "send everything to the senior"
- Mid-level engineers review AI PRs too - it's a learning opportunity

**5. Make it visible**
- Track review time and PR size per team (not per person)
- Talk about review load in retros

## Protecting Skill Development

The real long-term risk: engineers who can ship with AI but can't debug, design or reason without it - and juniors who never build the fundamentals.

### For junior engineers
- **Explain-back rule:** be able to explain any merged code line by line
- **Deliberate practice:** some tasks done without agents (agree which, e.g. first bug fix in a new area)
- **Use AI as a tutor:** "explain this", "what are the trade-offs", "what would break if" - not just "write this"
- **Pair with humans:** pairing and mob sessions still matter, maybe more
- **Debugging rotations:** production issues are where understanding is tested

### For everyone
- **Design stays human-owned:** use AI to explore options, humans decide and record in ADRs
- **Read the code:** periodic deep-dives into areas the team mostly touches via agents
- **On-call is a forcing function:** if nobody can debug a service at 3am, AI usage has outrun understanding

### Rethinking levels and career growth

What distinguishes levels is shifting from *output* to *judgement*:

| Skill | Becoming more important |
|-------|------------------------|
| Problem framing | Turning vague needs into precise, verifiable tasks (for humans and agents) |
| Verification | Knowing *how* to prove something works - tests, observability, rollout strategy |
| Review & taste | Spotting plausible-but-wrong code, over-engineering, missing edge cases |
| System design | Agents work within a design; someone has to own the design |
| Context engineering | Building the context files, tools and guardrails that make agents effective |
| Communication | Explaining trade-offs; AI makes code cheap, alignment is still expensive |

See [DevOps Career Ladder](./devops-career-ladder.md) and [Career Development](../leadership/career-development.md) - consider adding "effective, responsible use of AI tooling" and "context engineering" as expectations at each level.

## Measuring AI Impact Honestly

Leadership will ask "what's the ROI on AI?" Answer with system metrics, not vanity metrics.

### Vanity metrics - avoid
- ❌ "% of code written by AI"
- ❌ Lines of code / number of PRs
- ❌ Licence activation or "acceptance rate" alone
- ❌ Self-reported "hours saved" with no outcome check

These are easy to game and say nothing about value or quality.

### Better approach: measure the system before and after

Use the [Developer Productivity Metrics](./developer-productivity-metrics.md) framework you already have, and look at **throughput AND instability together**:

| Dimension | Metric | What you hope to see | Warning sign |
|-----------|--------|---------------------|--------------|
| Throughput | Change lead time, deployment frequency | Down / up | No change → bottleneck is elsewhere |
| Instability | Change fail rate, **rework rate** | Flat or down | Rising → speed is borrowed from quality |
| Flow | PR size, review wait time | Flat | Rising → review is the new bottleneck |
| Experience | Developer survey (friction, cognitive load, trust in AI) | Improving | Burnout or frustration rising |
| Impact | Time on new capability vs maintenance | More on new work | Same work, just faster rework |

**Method:**
1. Baseline before a rollout (or compare adopting vs not-yet-adopting teams)
2. Combine telemetry (pipeline, VCS) with a short quarterly survey
3. Review at 3 and 6 months - early numbers are noisy while people learn
4. Report outcomes to leadership in business terms ("lead time for customer features fell from X to Y with no rise in change fail rate")

**The honest answer is often:** "AI sped up coding; our next constraint is review/testing/deployment, and here's the investment to unlock it."

## Rolling Out AI Agents: A Phased Approach

### Phase 1: Foundations (weeks 1-4)
- [ ] Publish the team AI working agreement
- [ ] Approved tools licensed, accounts set up
- [ ] Baseline metrics captured
- [ ] Context file added to main repos
- [ ] CI quality gates reviewed (would they catch bad AI code?)

### Phase 2: Interactive use (months 1-3)
- [ ] Everyone using inline + interactive agents for daily work
- [ ] Weekly 15-min "show and tell" of what worked / didn't
- [ ] Shared prompt / technique library
- [ ] Review load and PR size watched closely

### Phase 3: Targeted automation (months 3-6)
- [ ] Pick 1-2 well-bounded use cases for background agents (dependency upgrades, test gaps, doc updates, flaky test fixes)
- [ ] AI first-pass code review on PRs
- [ ] MCP servers for key internal systems (with security review)
- [ ] Measure: did it reduce toil without raising rework?

### Phase 4: Scale and embed (6+ months)
- [ ] AI expectations in career ladder and onboarding
- [ ] Platform team owns AI tooling as a platform capability (golden path for agents: sandboxes, permissions, context, MCP catalogue)
- [ ] Regular review of policy and tools

## Platform Team Role

For platform / DevOps teams, AI is both a **tool you use** and a **capability you provide**:

**As a platform capability:**
- Approved, pre-configured agent environments (e.g. cloud dev environments / [Dev Box](./azure-devbox-defender.md) with tools installed)
- Secure secrets handling so agents never see credentials
- Curated MCP server catalogue with access controls
- Golden-path templates that include context files and quality gates
- Sandboxed, least-privilege identities for background agents
- Audit logging of agent actions in CI/CD and cloud

**As users:**
- IaC generation and review (Bicep / Terraform) - always review the plan/what-if
- Pipeline authoring and troubleshooting
- Incident investigation (log / trace summarisation) - human makes the call
- Runbook and documentation upkeep

This fits [Team Topologies](./team-topologies.md): an **enabling team** (or enabling function within the platform team) can coach stream-aligned teams on effective agent use, then step back.

## Security & Risk

| Risk | Mitigation |
|------|-----------|
| Secrets or customer data sent to AI tools | Approved tools with enterprise data terms; secret scanning; clear data rules |
| Prompt injection (agent reads malicious content in issues, docs, dependencies) | Least-privilege agent permissions; human review before merge/deploy; no auto-execution of untrusted instructions |
| Over-privileged agents | Scoped tokens, sandboxes, no production credentials, approval gates |
| Hallucinated dependencies ("slopsquatting") | Dependency allow-lists, lockfiles, supply-chain scanning |
| Insecure code patterns | SAST in CI, security review for sensitive areas |
| Licence / IP concerns | Company-approved tools with appropriate indemnity; follow legal guidance |
| Unvetted MCP servers | Treat as third-party software: review, pin versions, restrict access |

## Common Anti-Patterns

### ❌ Mandate and measure usage
Forcing adoption and tracking per-person usage creates theatre, not value. Measure team outcomes instead.

### ❌ Banning it
Engineers will use personal tools anyway - with worse data controls. Provide approved tools and clear rules.

### ❌ Expecting headcount savings on day one
Early gains get absorbed by learning, review load and rework. Plan for capability gains first.

### ❌ Bigger PRs because "the AI did it"
Batch size is still the strongest predictor of delivery stability.

### ❌ "The AI wrote it"
Ownership doesn't transfer. Blameless post-mortems still look at the *system* (why did review and tests miss it?), but the author owns the change.

### ❌ Ignoring the juniors
Short-term speed, long-term capability gap. Deliberately design learning in.

### ❌ AI strategy without platform strategy
Seven DORA capabilities, five of them are platform and practice. Fix the pipeline first.

## Conversations You'll Need to Have

**With your team:**
- "What's working, what's frustrating, where don't you trust it?" (retro topic)
- Agreeing the working agreement together, not imposing it

**With an engineer over-relying on AI:**
- Focus on observable outcomes: review quality, bugs, ability to explain changes
- Use [feedback models](../leadership/feedback-models.md) - SBI works well
- Agree specific practices (explain-back, deliberate no-AI tasks)

**With an engineer refusing to use AI:**
- Understand why (quality concerns? skill identity? past bad experience?) - often valid
- Pair them with an effective user on a well-suited task
- Expectation is effective use of team tools, not maximal use

**With leadership:**
- Frame as system improvement with measured outcomes
- Be honest about where the bottleneck now is
- Ask for investment in platform, testing and review capacity alongside licences

## Quick Reference

**Five rules:**
1. You own what you merge
2. Small batches, always
3. Same review bar for human and AI code
4. Measure the system, not the usage
5. Invest in the platform - it's what AI amplifies

**Monthly check:**
- [ ] PR size and review time stable?
- [ ] Change fail rate and rework rate stable or falling?
- [ ] Juniors growing real understanding?
- [ ] Working agreement still current?
- [ ] Team sentiment on AI tools (survey / retro)?

## Resources

### Reports & Research
- [ ] DORA 2025 "State of AI-assisted Software Development" report (dora.dev)
- [ ] DORA AI Capabilities Model (dora.dev)
- [ ] DX research on measuring AI impact (getdx.com)

### Books
- [ ] "Frictionless" by Nicole Forsgren & Abi Noda (2025)
- [ ] "Accelerate" by Nicole Forsgren, Jez Humble, Gene Kim

### Practices
- [ ] Model Context Protocol documentation (modelcontextprotocol.io)
- [ ] Your AI tool vendor's guidance on context files and agent security

### Related Guides
- [Developer Productivity Metrics](./developer-productivity-metrics.md)
- [Platform Engineering & DevEx](./platform-engineering-devex.md)
- [Team Topologies](./team-topologies.md)
- [DevOps Career Ladder](./devops-career-ladder.md)
- [Psychological Safety](./psychological-safety.md)

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

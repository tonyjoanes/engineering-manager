# Developer Productivity Metrics

How to measure engineering delivery and developer experience in 2026: DORA's current five metrics, the 2025 team profiles, SPACE, DevEx, and the DX Core 4 - and how to use them without wrecking trust.

## Why This Guide Exists

The measurement landscape has moved on from "the four DORA metrics with Elite/High/Medium/Low tiers":

| What changed | When | Why it matters |
|--------------|------|----------------|
| DORA added a fifth metric, **rework rate** | 2024 | Catches unplanned work caused by bad deploys - the hidden tax on speed |
| MTTR replaced by **failed deployment recovery time** | 2023-24 | Scoped to *deployments*, not all incidents (infra outages etc. are measured elsewhere) |
| Metrics grouped into **throughput** and **instability** | 2024 | Speed and stability are measured together, not traded off |
| **Seven team profiles** replace the four performance tiers | 2025 | Adds well-being, friction and burnout to the picture |
| **DORA AI Capabilities Model** | 2025 | What makes AI adoption pay off - see [AI-Assisted Engineering](./ai-assisted-engineering.md) |
| **DX Core 4** unifies DORA, SPACE and DevEx | 2024-25 | A single, exec-friendly set of four dimensions |

## Golden Rules

Before any framework:

1. **Measure teams and systems, never individuals.** Per-person productivity metrics destroy trust and get gamed (Goodhart's law).
2. **Pair opposing metrics.** Speed with stability, output with experience.
3. **Trends beat benchmarks.** Your own trajectory matters more than industry comparisons.
4. **Combine telemetry and surveys.** System data tells you *what*; developers tell you *why*.
5. **Every metric should drive a conversation or a decision.** If nobody acts on it, stop collecting it.
6. **Share with the team first.** Metrics are for the team to improve, not for management to judge.

## DORA: The Five Software Delivery Metrics

DORA (DevOps Research & Assessment, now part of Google Cloud) measures software delivery performance with five metrics in two groups.

### Throughput - how fast changes flow

**1. Change lead time**
- Time from code committed to running in production
- Shows: how efficient your path to production is
- Improve with: smaller batches, faster CI, automated deployment, less manual approval

**2. Deployment frequency**
- How often you deploy to production
- Shows: batch size and confidence in releasing
- Improve with: trunk-based development, feature flags, automated pipelines

**3. Failed deployment recovery time**
- Time to recover when a *deployment* causes a failure that needs immediate intervention
- Replaces the old "MTTR", which mixed in incidents unrelated to change
- Improve with: fast rollback, feature flags, progressive delivery, good observability

### Instability - how often changes cause problems

**4. Change fail rate**
- % of deployments that need immediate intervention (rollback, hotfix, fix-forward)
- Shows: quality of what reaches production

**5. Deployment rework rate** *(new)*
- % of deployments that are **unplanned** and happen *because of* a production incident
- Shows: how much of your delivery capacity is spent cleaning up
- Why it was added: a team can look fast on deployment frequency when many of those deploys are fixes for previous deploys

```
Rework rate = Unplanned deployments caused by production incidents / Total deployments × 100
```

### Key insight: speed and stability go together

DORA's research consistently finds that throughput and stability are **correlated, not traded off**. The best teams are fast *and* stable; struggling teams are usually slow *and* unstable. If someone says "we need to slow down to be stable", the fix is usually smaller batches, not fewer deploys.

### What about benchmarks?

DORA publishes cluster data each year, but the 2025 report moved away from the "Elite/High/Medium/Low" labels. Use these as **rough orientation only**:

| Metric | Strong teams typically | Struggling teams typically |
|--------|------------------------|----------------------------|
| Change lead time | Less than a day | More than a month |
| Deployment frequency | On demand (multiple per day) | Less than monthly |
| Failed deployment recovery time | Less than an hour | More than a week |
| Change fail rate | Low single-digit to ~15% | 40%+ |
| Rework rate | Low | High - significant share of deploys are fixes |

**Better:** use the free DORA Quick Check at dora.dev to compare against current data, then focus on your own trend.

### Measuring DORA in practice

| Metric | Data source | Notes |
|--------|------------|-------|
| Change lead time | VCS + pipeline (commit → prod deploy) | Use median, not mean |
| Deployment frequency | Pipeline deploy events | Count prod deploys per service |
| Failed deployment recovery time | Deploy events + incident / rollback records | Needs deploys linked to incidents |
| Change fail rate | Deploys marked as failed (rollback, hotfix, incident link) | Agree a definition of "failed" with the team |
| Rework rate | Deploys tagged as unplanned / incident-driven | Tag hotfix pipelines or link deploys to incident tickets |

**For Azure DevOps / GitHub:** pipeline run history gives frequency and lead time; tagging hotfix runs (or using a dedicated hotfix pipeline) and linking incidents to work items gives the instability metrics. Tools like DX, LinearB, Sleuth, Faros, and GitHub/Azure DevOps analytics can automate this.

## DORA 2025: Seven Team Profiles

The 2025 report clustered teams on delivery *and* human factors (well-being, burnout, friction, product performance) into seven profiles. Use them as a **diagnostic conversation**, not a label.

| Profile | Share | What it looks like | Where to focus |
|---------|-------|--------------------|----------------|
| **Foundational challenges** | ~10% | Struggling across the board: delivery, stability, well-being | Basics: CI/CD, version control, small batches, reduce WIP |
| **The legacy bottleneck** | ~11% | Constantly reacting to unstable systems; high friction | Stabilise, pay down the worst tech debt, invest in observability |
| **Constrained by process** | ~17% | Stable tech, but bureaucracy, meetings and approvals slow everything; high burnout | Remove process: approval gates, meetings, hand-offs |
| **High impact, low cadence** | ~7% | Great outcomes via heroics; shaky delivery foundation | Make success repeatable: automation, shared knowledge, sustainable pace |
| **Stable and methodical** | ~15% | Reliable and proud of their work, but slower | Safe speed-ups: smaller batches, more automation, progressive delivery |
| **Pragmatic performers** | ~20% | Fast and stable, but well-being and engagement only average | Team health: autonomy, recognition, reduce friction |
| **Harmonious high-achievers** | ~20% | Fast, stable, healthy and engaged | Protect it; share practices with other teams |

**How to use:**
- In a retro or team health session, show the profiles and ask "which one sounds most like us, and why?"
- Compare the team's view with the metrics
- Pick one improvement from the "where to focus" column

See also: [Team Health Metrics](./team-health-metrics.md), [Retrospectives](./retrospectives.md), [Burnout Prevention](../heuristics/burnout-prevention.md).

## SPACE: The Dimensions of Productivity

SPACE (Forsgren, Storey et al., 2021) is a **framework for choosing metrics**, not a metric set. It says productivity has five dimensions and you need several of them:

| Dimension | Example metrics |
|-----------|-----------------|
| **S**atisfaction & well-being | Survey: satisfaction, burnout, would recommend team |
| **P**erformance | Outcomes: quality, reliability, customer impact |
| **A**ctivity | Counts: PRs, deploys, reviews (team level only, never alone) |
| **C**ommunication & collaboration | Review turnaround, knowledge sharing, onboarding time |
| **E**fficiency & flow | Uninterrupted focus time, hand-offs, wait time |

**Rule of thumb:** pick metrics from at least three dimensions, including at least one perceptual (survey) measure.

## DevEx: What Developers Actually Feel

The DevEx framework (Noda, Storey, Forsgren, Greiler, 2023) identifies three core dimensions of developer experience:

**1. Feedback loops** - how fast do developers get answers?
- Build and test times, code review turnaround, deploy time, time to get questions answered

**2. Cognitive load** - how much do developers have to hold in their heads?
- Codebase complexity, documentation quality, number of tools, unclear processes

**3. Flow state** - can developers get into deep work?
- Interruptions, meeting load, unplanned work, on-call noise

Measure each with **both** a system metric and a survey question, e.g. "CI time p50" + "How satisfied are you with the speed of our CI?"

See [Platform Engineering & DevEx](./platform-engineering-devex.md) for how to improve these.

## DX Core 4: Putting It Together

The DX Core 4 (Abi Noda & Laura Tacho, DX, 2024) combines DORA, SPACE and DevEx into **four dimensions** that make sense to engineers *and* to the CFO.

| Dimension | Key metric | Secondary metrics |
|-----------|-----------|-------------------|
| **Speed** | Diffs (PRs) per engineer - **team-level only** | Lead time, deployment frequency, perceived rate of delivery |
| **Effectiveness** | Developer Experience Index (DXI) - survey-based | Time to 10th PR (onboarding), ease of delivery, regretted attrition |
| **Quality** | Change fail rate | Failed deployment recovery time, perceived software quality, operational health |
| **Impact** | % of time spent on new capabilities | Initiative progress / ROI, revenue per engineer, R&D as % of revenue |

**Why it's useful:**
- **Oppositional by design:** Speed is balanced by Effectiveness and Quality, so pushing one at the expense of others shows up
- **Business language:** "Impact" connects engineering to things leadership already tracks
- **Lightweight start:** can begin with a survey plus pipeline data in a few weeks

**Caution:** "diffs per engineer" is the most misused metric in the set. Never look at it per person, never set targets on it, and always show it next to DXI and change fail rate.

## Which Framework When?

| Situation | Use |
|-----------|-----|
| "How good is our delivery pipeline?" | DORA five metrics |
| "Why does the team feel slow / frustrated?" | DevEx dimensions + survey |
| "We're choosing metrics and don't want to get it wrong" | SPACE as a checklist |
| "Leadership wants one view of engineering productivity" | DX Core 4 |
| "Is our team healthy overall?" | DORA team profiles + [Team Health Metrics](./team-health-metrics.md) |
| "Is AI paying off?" | DORA throughput + instability before/after, plus survey - see [AI-Assisted Engineering](./ai-assisted-engineering.md#measuring-ai-impact-honestly) |
| "Is our platform working?" | DevEx metrics + platform adoption - see [Platform Engineering & DevEx](./platform-engineering-devex.md) |

**They're complementary, not competing.** A sensible default for most teams:
- DORA five metrics from pipeline data (automated, monthly)
- A short quarterly developer survey covering DevEx dimensions
- DX Core 4 as the summary for leadership

## Setting Up a Measurement Programme

### Step 1: Start with the question
"What decision will this help us make?" e.g. "Where should the platform team invest next quarter?"

### Step 2: Baseline (2-4 weeks)
- [ ] Pull DORA metrics from pipelines for the last 3 months
- [ ] Run a short developer survey (10-15 questions, anonymous)
- [ ] Agree definitions with the team (what is a "failed" deploy? what counts as "rework"?)

### Step 3: Share and discuss
- [ ] Present to the team first
- [ ] Ask: "Does this match how it feels?" Mismatches are the most interesting findings
- [ ] Pick 1-2 improvements

### Step 4: Review regularly
- **Monthly:** DORA trends in team review
- **Quarterly:** survey + profile discussion + leadership summary
- **Yearly:** are these still the right metrics?

### Sample survey questions

Use a 1-5 scale. Keep it short so people actually answer.

- How easy is it to deliver a change to production?
- How satisfied are you with build and test speed?
- How often are you able to get into a state of deep focus?
- How easy is it to understand the code you work on?
- How much of your time last month went on unplanned work?
- How confident are you that a deploy won't break production?
- How much do you trust the output of AI tools you use? *(if relevant)*
- What's the single biggest thing slowing you down? *(free text)*

## Anti-Patterns

### ❌ Individual leaderboards
Ranking engineers by PRs, commits or "diffs" - the fastest way to destroy collaboration and data quality.

### ❌ Targets on DORA metrics
"Deploy 10x per day by Q3" leads to meaningless deploys. Targets go on outcomes; metrics show progress.

### ❌ Comparing teams with different contexts
A legacy mainframe team and a greenfield web team shouldn't be ranked on lead time.

### ❌ Metrics without surveys
Telemetry misses friction, cognitive load and burnout - the things DORA's 2025 profiles show matter.

### ❌ Ignoring instability when chasing speed
Deployment frequency up + rework rate up = treadmill, not progress.

### ❌ Old benchmarks as gospel
The Elite/High/Medium/Low tiers came from specific survey years. Use current data and your own trend.

## Quick Reference

```
DORA throughput:  Change lead time · Deployment frequency · Failed deployment recovery time
DORA instability: Change fail rate · Rework rate
DevEx:            Feedback loops · Cognitive load · Flow state
SPACE:            Satisfaction · Performance · Activity · Collaboration · Efficiency
DX Core 4:        Speed · Effectiveness · Quality · Impact
```

## Resources

### Reports & Research
- [ ] DORA metrics guide and Quick Check (dora.dev)
- [ ] DORA 2024 Accelerate State of DevOps Report
- [ ] DORA 2025 State of AI-assisted Software Development Report
- [ ] "The SPACE of Developer Productivity" (ACM Queue, 2021)
- [ ] "DevEx: What Actually Drives Productivity" (ACM Queue, 2023)
- [ ] DX Core 4 (getdx.com)

### Books
- [ ] "Accelerate" by Nicole Forsgren, Jez Humble, Gene Kim
- [ ] "Frictionless" by Nicole Forsgren & Abi Noda (2025)

### Related Guides
- [Team Health Metrics](./team-health-metrics.md)
- [Platform Engineering & DevEx](./platform-engineering-devex.md)
- [AI-Assisted Engineering](./ai-assisted-engineering.md)
- [Incident Management](./incident-management.md)

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

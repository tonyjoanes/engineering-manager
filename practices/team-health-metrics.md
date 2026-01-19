# Team Health Metrics

Measuring and tracking the indicators that matter for team performance and wellbeing.

## Why Measure Team Health?

**What gets measured gets improved:**
- Identify problems early
- Track progress over time
- Make data-driven decisions
- Justify resources and changes
- Celebrate improvements

**Balance:**
- Too few metrics → Flying blind
- Too many metrics → Analysis paralysis
- Right metrics → Actionable insights

## Categories of Metrics

### 1. Delivery Metrics
How effectively the team ships work

### 2. Quality Metrics
How good the work is

### 3. Team Satisfaction Metrics
How people feel

### 4. Collaboration Metrics
How well the team works together

### 5. Growth Metrics
How the team is developing

## Delivery Metrics

### Velocity / Throughput

**What it measures:** Amount of work completed per time period

**How to track:**
- Story points per sprint (Scrum)
- Number of tickets completed per week
- Features shipped per quarter

**Use for:**
- Planning capacity
- Spotting trends
- Forecasting timelines

**Don't use for:**
- Comparing teams (different contexts)
- Individual performance (team metric)
- Pressuring for more output

**Healthy velocity:**
- Consistent over time (± 15%)
- Sustainable (not burning out)
- Predictable for planning

**Red flags:**
- Wildly inconsistent sprint to sprint
- Declining over time
- Artificially inflated (gaming the metric)

### Cycle Time

**What it measures:** Time from work starting to work completing

**Typical stages:**
- Idea → Backlog
- Backlog → In Progress
- In Progress → Code Review
- Code Review → Deployed
- Deployed → Validated

**What to track:**
- Total cycle time (idea to production)
- Development time (code start to PR)
- Review time (PR submitted to approved)
- Deployment time (approved to production)

**Good cycle time:**
- Features: 1-2 weeks
- Bugs: 1-3 days
- Small fixes: Hours to 1 day

**Long cycle times indicate:**
- Too much WIP (work in progress)
- Blocked work
- Slow reviews
- Complex deployment process
- Unclear requirements

**How to improve:**
- Limit WIP
- Smaller work chunks
- Faster code reviews
- Automate deployment
- Better planning

### Lead Time

**What it measures:** Time from idea to customer value

**Different from cycle time:**
- Lead time: Customer perspective (request to delivery)
- Cycle time: Team perspective (start to done)

**Track:**
- Feature requests → production
- Bug reports → fix deployed
- Customer asks → delivered

**Matters for:**
- Customer satisfaction
- Time to market
- Competitive advantage

### Deployment Frequency

**What it measures:** How often you ship to production

**Benchmarks (DORA metrics):**
- Elite: Multiple times per day
- High: Once per day to once per week
- Medium: Once per week to once per month
- Low: Less than once per month

**Why it matters:**
- Faster feedback
- Smaller changes (less risk)
- More agile
- Better MTTR (Mean Time To Recovery)

**How to improve:**
- Automate deployment
- Reduce deployment risk
- Feature flags
- CI/CD pipeline
- Smaller changes

### Change Failure Rate

**What it measures:** Percentage of deployments causing issues

**Calculate:**
```
(Failed deployments / Total deployments) × 100
```

**Benchmarks:**
- Elite: 0-15%
- High: 16-30%
- Medium: 31-45%
- Low: >45%

**What counts as failure:**
- Rollback required
- Production hotfix needed
- Significant degradation
- Customer-impacting bugs

**How to improve:**
- Better testing
- Staging environment
- Automated tests
- Code review quality
- Feature flags (test in production safely)

## Quality Metrics

### Bug Escape Rate

**What it measures:** Bugs reaching production vs caught before

**Track:**
- Bugs found in code review
- Bugs found in QA/staging
- Bugs found in production
- Severity of bugs

**Calculate:**
```
Production bugs / (Total bugs found + Production bugs) × 100
```

**Target:** <10% of bugs reach production

**High escape rate indicates:**
- Insufficient testing
- Poor code review
- Rushed work
- Complex code
- Unclear requirements

### Technical Debt

**What it measures:** Accumulation of shortcuts and suboptimal code

**How to track:**
- SonarQube/CodeClimate scores
- Code complexity metrics
- Test coverage percentage
- Number of TODO/FIXME comments
- Time spent on maintenance vs features

**Monitor:**
- Trend over time (growing or shrinking?)
- Time to onboard new engineers (debt slows this)
- Developer satisfaction (debt frustrates)

**Healthy balance:**
- Some debt is okay (trade-offs happen)
- Dedicate 10-20% of time to paying it down
- Don't let it grow unbounded

### Test Coverage

**What it measures:** Percentage of code covered by automated tests

**Types:**
- Line coverage
- Branch coverage
- Function coverage

**Targets:**
- 70-80% is good
- 100% is overkill
- <50% is concerning

**Don't:**
- Game the metric (meaningless tests)
- Test for test's sake
- Mandate 100% (diminishing returns)

**Do:**
- Test critical paths
- Test complex logic
- Test edge cases
- Make tests meaningful

### Code Review Quality

**What to track:**
- Time to first review
- Number of review rounds
- Comments per PR
- Approval rate

**Good indicators:**
- First review within 24 hours
- 1-2 review rounds typical
- Constructive comments
- Balance of approval vs requests for changes

**Red flags:**
- PRs sitting for days
- Rubber-stamp approvals
- Hostile review comments
- Always requiring many rounds

## Team Satisfaction Metrics

### eNPS (Employee Net Promoter Score)

**The question:**
"On a scale of 0-10, how likely are you to recommend working here to a friend?"

**Calculate:**
- Promoters (9-10): Happy, engaged
- Passives (7-8): Satisfied but not enthusiastic
- Detractors (0-6): Unhappy, at risk
- eNPS = % Promoters - % Detractors

**Benchmarks:**
- >50: Excellent
- 10-50: Good
- 0-10: Needs work
- <0: Crisis

**Frequency:** Quarterly

### Team Satisfaction Survey

**Regular pulse questions (monthly):**

Rate 1-5:
- I feel productive and effective
- I have the tools and resources I need
- I understand team priorities
- I feel supported by my manager
- I'm learning and growing
- I feel valued for my contributions
- Work-life balance is sustainable
- I see a future for myself here

**Open-ended:**
- What's going well?
- What could be better?
- What's blocking you?

### Retention Rate

**What it measures:** People staying vs leaving

**Calculate:**
```
(Team members at end / Team members at start) × 100
```

**Measure over:**
- 1 year: Annual retention
- Voluntary vs involuntary
- By tenure (losing new hires vs senior?)

**Benchmarks:**
- >90% annual: Healthy
- 80-90%: Industry average
- <80%: Problem

**Watch for:**
- Losing high performers
- Losing diverse talent
- Exit trends (why are they leaving?)

### Sick Days / PTO Usage

**What to track:**
- Sick days taken
- PTO taken vs accrued
- Patterns (same people, same times)

**Red flags:**
- Nobody taking PTO (burnout brewing)
- Excessive sick days (burnout or health issues)
- PTO accrual growing (not taking breaks)

**Healthy:**
- People take their PTO
- Sick days are occasional, not chronic
- No guilt about time off

## Collaboration Metrics

### Code Review Participation

**What to track:**
- Who's reviewing code?
- Review distribution (everyone or few people?)
- Response times
- Quality of reviews

**Good distribution:**
- Everyone reviews code
- No single bottleneck
- Cross-pollination of knowledge

**Bad patterns:**
- Only senior people review
- Same person always reviews
- Reviews ignored or delayed

### Meeting Load

**Track:**
- Hours in meetings per person per week
- Meeting efficiency (was it useful?)
- Who's in too many meetings?

**Healthy:**
- Individual contributors: 10-15 hours/week
- Managers: 20-25 hours/week
- More than that: Probably too many

**Audit meetings:**
- Does this meeting need to exist?
- Are the right people there?
- Can it be shorter?
- Can it be async?

### Collaboration Score

**Survey questions:**
- I can easily get help when blocked
- Information is shared openly
- We collaborate well cross-functionally
- Conflicts are resolved constructively
- I trust my teammates

**Track trends:**
- Improving or declining?
- Which areas are weakest?
- Impact of changes made

## Growth Metrics

### Skills Development

**Track:**
- Training completed
- Certifications earned
- New technologies learned
- Conference attendance
- Books read (eng book club)

**Qualitative:**
- Self-assessment of skill growth
- Manager assessment
- Peer feedback on growth

### Career Progression

**Monitor:**
- Promotions per year
- Time in each level
- Promotion pipeline (ready for promotion)
- Reasons for lack of promotion

**Healthy:**
- Clear promotion criteria
- Regular promotions (not everyone, but some)
- Diverse people being promoted
- Transparent process

### Knowledge Sharing

**Track:**
- Tech talks given
- Documentation created
- Blog posts written
- Mentorship hours
- Lunch and learns

**Why it matters:**
- Develops presenters
- Spreads knowledge
- Builds culture
- Reduces bus factor

## How to Collect Metrics

### Automated Tools

**From systems:**
- Jira/Linear: Velocity, cycle time, throughput
- GitHub/GitLab: PR metrics, deployment frequency
- CI/CD: Build times, test results, deployment success
- Monitoring: Incident frequency, MTTR
- Code quality: SonarQube, CodeClimate

**Advantages:**
- Automatic collection
- Historical data
- Objective
- Low effort

### Surveys

**Tools:**
- Google Forms
- Officevibe
- TinyPulse
- Culture Amp
- Custom

**Tips:**
- Keep surveys short (5-10 questions)
- Mix quantitative and qualitative
- Anonymous option for honesty
- Regular cadence (monthly pulse, quarterly deep)
- Act on feedback (or stop surveying)

### 1:1 Conversations

**Qualitative insights:**
- How people really feel
- Context behind numbers
- Early warning signs
- Suggestions for improvement

**Ask:**
- How are you feeling about work?
- What's frustrating you?
- What would make things better?
- Where are you blocked?

## Dashboards and Reporting

### Create a Team Health Dashboard

**Components:**
- Key metrics with trends
- Green/yellow/red indicators
- Targets and actual
- Historical comparison

**Share with:**
- The team (transparency)
- Leadership (visibility)
- Other teams (benchmarking)

**Update frequency:**
- Real-time: Automated metrics
- Weekly: Cycle time, velocity
- Monthly: Satisfaction surveys
- Quarterly: Deep dives

### Example Dashboard

```
Team Health Dashboard - [Team Name] - [Date]

📊 Delivery
✓ Velocity: 42 points (target: 40)
✓ Cycle Time: 8 days (target: <10)
⚠ Deployment Frequency: 2x/week (target: daily)

🐛 Quality
✓ Bug Escape Rate: 8% (target: <10%)
✓ Test Coverage: 75% (target: >70%)
✓ Change Failure Rate: 12% (target: <15%)

😊 Satisfaction
✓ eNPS: 45 (was 40 last quarter)
⚠ Work-Life Balance: 3.2/5 (was 3.8)
⚠ PTO Usage: 45% of accrued (target: >70%)

🤝 Collaboration
✓ Code Review Time: 6 hours avg (target: <24h)
✓ Meeting Load: 14 hours/week (target: <15)
✓ Collaboration Score: 4.2/5

📈 Growth
✓ 2 promotions this quarter
✓ 5 tech talks given
⚠ Training completion: 60% (target: 80%)
```

## Acting on Metrics

### When Metrics Are Bad

**Don't panic:**
- One bad week isn't a trend
- Look for patterns over time
- Understand context

**Investigate:**
- Why is this metric bad?
- What changed recently?
- Ask the team
- Look at correlated metrics

**Take action:**
- Address root cause, not symptoms
- Get team input on solutions
- Try experiments
- Measure impact of changes

**Example: Cycle Time Increasing**

Investigation:
- "Why is cycle time up from 5 days to 12 days?"
- Look at data: Code review time doubled
- Ask team: "Only two people reviewing, both on vacation last week"

Action:
- Increase reviewer pool
- Set review time expectations
- Automate review reminders
- Pair more people to spread knowledge

Measure:
- Did cycle time improve?
- Is review distribution better?
- Team satisfaction with reviews?

### When Metrics Are Good

**Don't stop measuring:**
- Metrics can regress
- Stay vigilant
- Maintain good practices

**Celebrate:**
- Recognize the team
- Share with leadership
- Understand what's working
- Replicate on other teams

**Level up:**
- Can we do even better?
- What's the next challenge?
- New metrics to track?

## Common Metric Mistakes

### ❌ Vanity Metrics

Metrics that look good but don't drive behavior:
- Lines of code written
- Hours worked
- Number of commits
- PRs opened (but not merged)

**Fix:** Measure outcomes, not activity

### ❌ Gaming the System

When metrics become targets:
- Inflating story points for velocity
- Meaningless tests for coverage
- Small PRs that should be one
- Working weekends to hit deadline (then burnout)

**Goodhart's Law:** "When a measure becomes a target, it ceases to be a good measure."

**Fix:**
- Multiple metrics (balance)
- Qualitative + quantitative
- Focus on outcomes
- Team discussion of metrics

### ❌ Too Many Metrics

Tracking 50 things = tracking nothing

**Fix:**
- 3-5 key metrics per category
- 10-15 total maximum
- Focus on actionable
- Review quarterly (remove/add)

### ❌ No Action

Collecting data but never using it

**Fix:**
- Monthly metric reviews
- Action items from trends
- Share insights with team
- Make decisions based on data

### ❌ Comparing Teams

"Team A has better velocity than Team B"

**Problems:**
- Different contexts
- Different work types
- Different definitions
- Creates toxic competition

**Fix:**
- Compare team to itself over time
- Focus on trends
- Celebrate improvements
- Collaboration, not competition

## Recommended Starter Metrics

**If you track nothing else, start here:**

1. **Team Satisfaction** (monthly survey)
   - Simple 5-question pulse

2. **Velocity/Throughput** (from ticket system)
   - How much work are we completing?

3. **Cycle Time** (from ticket system)
   - How long does work take?

4. **Bug Escape Rate** (track bugs)
   - How much reaches production?

5. **Retention** (manual)
   - Who's staying vs leaving?

**Then expand based on problems you're seeing.**

## Resources

- [ ] "Accelerate" by Nicole Forsgren, Jez Humble, Gene Kim (DORA metrics)
- [ ] "Measuring and Managing Performance in Organizations" by Robert Austin
- [ ] State of DevOps Reports (annual, free)
- [ ] SPACE framework (developer productivity metrics)

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

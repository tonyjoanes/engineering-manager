# Incident Management & Post-Mortems

Handling production incidents and learning from them effectively.

## What is an Incident?

**Definition:** An unplanned interruption or reduction in quality of service

**Examples:**
- Service outage
- Performance degradation
- Data corruption
- Security breach
- Significant bug affecting customers

**Not every bug is an incident** - incidents impact customers or business significantly.

## Incident Severity Levels

**Sev 1 (Critical):**
- Complete service outage
- Data loss
- Security breach
- All customers affected
- Response: Immediate, all hands

**Sev 2 (High):**
- Major functionality broken
- Significant customer impact
- Performance severely degraded
- Response: Within 30 min

**Sev 3 (Medium):**
- Minor functionality broken
- Some customers affected
- Workaround available
- Response: Within 2 hours

**Sev 4 (Low):**
- Cosmetic issues
- Minimal impact
- Can wait for normal fix
- Response: Next business day

## Incident Response Process

### 1. Detection

**How incidents are found:**
- Monitoring alerts
- Customer reports
- Internal discovery
- Third-party notifications

**Key:** Detect quickly - monitoring is critical

### 2. Declaration

**Who can declare:**
- Anyone who sees it
- On-call engineer
- Manager
- Customer support

**Err on side of declaring** - better safe than sorry

**Actions:**
- Create incident channel (#incident-YYYY-MM-DD-description)
- Page on-call
- Update status page
- Notify stakeholders

### 3. Assignment

**Incident Commander (IC):**
- Coordinates response
- Makes decisions
- Communicates status
- Doesn't have to fix it

**Roles:**
- IC (Incident Commander)
- Responders (fix the issue)
- Communications (update stakeholders)
- Scribe (document timeline)

**For Sev 1/2:** Clearly assign roles
**For Sev 3/4:** May be just one person

### 4. Investigation

**Gather information:**
- When did it start?
- What changed recently?
- What's the impact?
- What does monitoring show?
- Any recent deployments?

**Debug:**
- Check logs
- Review metrics
- Inspect database
- Look at recent changes

**Don't blame** - focus on fixing

### 5. Mitigation

**Goal:** Restore service quickly

**Options:**
- Rollback recent change
- Apply quick fix
- Route around problem
- Scale resources
- Disable feature

**Perfect fix can wait** - mitigation first, root cause later

### 6. Resolution

**Service restored:**
- Monitoring confirms
- Customers can use service
- Normal operation resumed

**Declare resolved:**
- Update status page
- Notify stakeholders
- Thank responders
- Schedule post-mortem

### 7. Post-Mortem

**Learn and prevent recurrence:**
- What happened?
- Why did it happen?
- How do we prevent it?

**Blameless analysis** - focus on systems, not people

See Post-Mortem section below.

## Incident Commander Role

### Responsibilities

**Coordinate:**
- Assign tasks
- Track progress
- Remove obstacles
- Make decisions

**Communicate:**
- Status updates
- Stakeholder notifications
- Leadership briefings
- Customer communications

**Document:**
- Timeline of events
- Actions taken
- Decisions made
- People involved

**Close:**
- Declare resolution
- Hand off to post-mortem
- Thank team

### IC Best Practices

**Stay calm:**
- You set the tone
- Panic spreads
- Breathe

**Be decisive:**
- Make calls quickly
- Don't overthink
- Can course-correct

**Delegate:**
- You coordinate, not fix
- Trust responders
- Focus on overview

**Communicate frequently:**
- Every 30 minutes minimum
- More for Sev 1
- Even if "no update"

**Don't assign blame:**
- Not helpful during incident
- Psychological safety matters
- Fix first, learn later

## Communication During Incidents

### Internal Communication

**Incident channel:**
- All discussion here
- No DMs (information silo)
- @mention for attention
- Thread major topics

**Status updates:**
- Regular cadence
- What we know
- What we're doing
- ETA if possible

**Stakeholder updates:**
- Leadership channel
- Customer support
- Product managers
- As needed

### External Communication

**Status page:**
- Update immediately
- Be transparent
- Regular updates
- Avoid technical jargon

**Customer communication:**
- Through support channels
- Acknowledge issue
- Set expectations
- Don't overpromise

**Social media:**
- If appropriate
- Consistent with status page
- Professional tone

**Example status update:**
"We're investigating reports of slow load times. Our team is actively working on this. We'll update within 30 minutes."

## Post-Mortem Process

### What is a Post-Mortem?

**Blameless analysis of incident to:**
- Understand what happened
- Identify root causes
- Prevent recurrence
- Improve response

**Blameless means:**
- No finger-pointing
- Focus on systems, not people
- Assume good intent
- Learn, don't punish

### When to Do Post-Mortems

**Always for:**
- Sev 1 and Sev 2
- Any customer data loss
- Security incidents
- Repeated issues

**Consider for:**
- Sev 3 if interesting learnings
- Near misses
- Novel situations

### Post-Mortem Timeline

**Within 24-48 hours:**
- Schedule meeting
- Assign owner
- Gather data

**Within 1 week:**
- Draft completed
- Meeting held
- Action items assigned

**Within 2 weeks:**
- Published and shared
- Action items in progress

**Strike while memory is fresh.**

### Post-Mortem Template

```markdown
# Post-Mortem: [Brief Description]

**Date:** [Incident date]
**Authors:** [Names]
**Status:** [Draft / Review / Published]
**Severity:** [1/2/3/4]
**Duration:** [Start time] - [End time] ([X hours/minutes])
**Impact:** [Number of users, revenue impact, etc.]

## Summary
[2-3 sentence overview of what happened]

## Timeline
All times in [timezone]

- **HH:MM** - [Event]
- **HH:MM** - [Event]
- **HH:MM** - [Event]

## Root Cause
[Deep dive into the fundamental cause, not just proximate trigger]

## Detection
[How was the incident detected? How long between start and detection?]

## Resolution
[What fixed it? How long to fix?]

## Impact
- **Users affected:** [Number or percentage]
- **Duration:** [Length of outage]
- **Revenue impact:** [If applicable]
- **Data impact:** [Any data lost/corrupted]

## What Went Well
- [Thing that helped]
- [Thing that helped]

## What Went Wrong
- [Thing that didn't work]
- [Thing that made it worse]

## Action Items
- [ ] [Action] - Owner: [Name] - Due: [Date]
- [ ] [Action] - Owner: [Name] - Due: [Date]
- [ ] [Action] - Owner: [Name] - Due: [Date]

## Lessons Learned
[Key takeaways and insights]
```

### Post-Mortem Meeting

**Who attends:**
- Incident responders
- IC
- Manager
- Relevant stakeholders
- Anyone interested (open invite)

**Format (60 min):**
- 5 min: Context and overview
- 10 min: Walk through timeline
- 20 min: Discuss root causes
- 20 min: Generate action items
- 5 min: Wrap up

**Facilitator role:**
- Keep discussion productive
- Redirect blame to systems
- Ensure psychological safety
- Capture action items

### Blameless Culture

**Redirect from people to systems:**

❌ "Why didn't you check the logs?"
✓ "Why didn't our monitoring alert us?"

❌ "You should have known better"
✓ "How can we make this knowledge more accessible?"

❌ "Who deployed this?"
✓ "What in our deployment process allowed this?"

**Focus on:**
- What in our systems failed?
- What processes need improvement?
- What knowledge was missing?
- How do we prevent recurrence?

### Action Items

**Good action items:**
- Specific and actionable
- Assigned to one person
- Have due dates
- Address root cause
- Prioritized

**Types:**
- Monitoring improvements
- Process changes
- Technical fixes
- Documentation updates
- Training needs

**Track completion:**
- Review in team meetings
- Follow up on overdue
- Celebrate completion
- Measure effectiveness

### Sharing Post-Mortems

**Share widely:**
- Engineering organization
- Relevant stakeholders
- Company all-hands (if major)
- Public blog (sometimes)

**Why share:**
- Organizational learning
- Transparency
- Demonstrate learning culture
- Help other teams
- Build trust

**Examples of public post-mortems:**
- AWS, Google, GitHub all publish major ones
- Shows customer respect
- Industry learning

## Incident Prevention

### Defense in Depth

**Multiple layers:**
- Monitoring and alerting
- Automated testing
- Code review
- Staging environments
- Gradual rollouts
- Feature flags
- Circuit breakers
- Graceful degradation

### Monitoring

**What to monitor:**
- Service availability
- Error rates
- Response times
- Resource usage (CPU, memory, disk)
- Business metrics
- Dependencies

**Alert on:**
- Anomalies
- Threshold breaches
- Trends (degrading over time)

**Alert philosophy:**
- Page on user impact
- Log everything else
- Reduce noise
- Make actionable

### Runbooks

**Document common issues:**
- Symptoms
- Investigation steps
- Resolution procedures
- Escalation paths

**Keep updated:**
- Review quarterly
- Update after incidents
- Easy to find
- Test procedures

## On-Call

**See [On-Call Best Practices](./on-call.md) for full details.**

**Key points:**
- Rotation schedule
- Clear escalation
- Compensation (pay or time off)
- Handoff procedures
- Support for on-call engineers

## Incident Metrics

**Track:**
- MTTR (Mean Time To Recovery)
- MTTD (Mean Time To Detection)
- Incident frequency
- Severity distribution
- Repeat incidents

**Use to:**
- Identify patterns
- Measure improvement
- Justify investments
- Set goals

## Common Mistakes

### ❌ Blame Culture
Punishing mistakes means hiding them

### ❌ No Post-Mortems
Missing learning opportunity

### ❌ Action Items Not Completed
Post-mortem theater - writing but not doing

### ❌ Heroics Culture
Celebrating firefighting instead of fire prevention

### ❌ Poor Communication
Stakeholders surprised or uninformed

### ❌ Perfectionism in Mitigation
Spending hours on perfect fix instead of quick rollback

## Resources

- [ ] "Site Reliability Engineering" by Google (free online)
- [ ] "Incident Management for Operations" by Rob Schnepp
- [ ] "The Phoenix Project" by Gene Kim
- [ ] PagerDuty Incident Response documentation

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

# On-Call Best Practices

Running sustainable and effective on-call rotations.

## What is On-Call?

**Definition:** Being available to respond to production issues outside normal working hours.

**Responsibilities:**
- Respond to pages/alerts
- Investigate and mitigate incidents
- Escalate when needed
- Document issues
- Participate in post-mortems

## Setting Up On-Call

### Rotation Schedule

**Common patterns:**
- Weekly rotation
- Weekday vs weekend split
- Follow-the-sun (global teams)
- Primary + secondary backup

**Considerations:**
- Team size (need 4+ for sustainable rotation)
- Coverage hours (24/7 or business hours only)
- Handoff timing (Monday morning works well)
- Holiday coverage

### Eligibility

**Who should be on-call:**
- Engineers familiar with systems
- Completed training
- Access to tools and systems
- Comfortable with responsibility

**New engineers:**
- Shadow rotation first (observe, don't respond)
- Paired with experienced engineer
- Gradual responsibility increase

### Compensation

**Fair compensation required:**
- On-call stipend (even if not paged)
- Overtime pay for actual incidents
- Time-in-lieu (extra PTO)
- Combination approach

**Don't:** Expect free on-call labor

## On-Call Readiness

### Documentation

**Runbooks for common issues:**
- Symptoms and diagnostics
- Step-by-step resolution
- Escalation procedures
- Contact information

**Keep updated:**
- Review quarterly
- Update after incidents
- Easy to find
- Test procedures work

### Tools Access

**Ensure on-call has:**
- VPN access
- Production system access
- Monitoring dashboards
- PagerDuty/alerting system
- Communication tools (Slack, Zoom)
- Deployment tools (if needed)

### Training

**Before first rotation:**
- System architecture overview
- Common issues and fixes
- Tools training
- Incident response process
- Practice scenarios

## During On-Call

### Response Expectations

**Response times:**
- Critical (Sev 1): 15 minutes
- High (Sev 2): 30 minutes
- Medium (Sev 3): 1 hour
- Low (Sev 4): Next business day

**Acknowledge quickly:**
- Let system know you got the page
- Prevents escalation
- Reduces anxiety

### Investigation

**First steps:**
1. Acknowledge the alert
2. Assess severity
3. Check monitoring/logs
4. Review recent changes
5. Start incident channel if needed

**Communicate:**
- Update incident channel
- Status page if customer-facing
- Escalate if needed

### Escalation

**Know when to escalate:**
- Beyond your expertise
- Not making progress in 30 min
- Severity higher than initially thought
- Need additional help

**How to escalate:**
- Page secondary on-call
- Contact specific expert
- Wake up manager (if truly critical)
- Follow escalation runbook

**Don't be a hero** - escalate when needed

## Handoff

### Handoff Meeting

**At rotation change:**
- Outgoing summarizes week
- Any ongoing issues
- Notable incidents
- Action items
- Questions from incoming

**Duration:** 15-30 minutes

### Handoff Document

**Template:**
```
On-Call Handoff - Week of [Date]

Ongoing Issues:
- [Issue]: [Status and next steps]

Incidents This Week:
- [Date]: [Brief description]
- [Date]: [Brief description]

System Health:
- [Service]: [Status/concerns]
- [Service]: [Status/concerns]

Action Items:
- [ ] [Item] - [Owner]

Notes:
[Anything else incoming should know]

Contact: [Outgoing engineer contact info]
```

## Supporting On-Call Engineers

### Manager Responsibilities

**During their rotation:**
- Check in daily
- Available for escalation
- Recognize their service
- Shield from other work

**After incidents:**
- Debrief conversation
- Time to recover
- Appreciation
- Post-mortem support

**Overall:**
- Ensure fair rotation
- Adequate compensation
- Training provided
- Sustainable workload

### Reducing Burden

**Minimize pages:**
- Fix root causes
- Improve monitoring (reduce noise)
- Automate responses
- Self-healing systems

**Every page is a failure of automation.**

### Recovery Time

**After significant incident:**
- Time off next day
- Adjusted workload
- No pressure
- Acknowledge impact

**Don't:** Expect normal productivity after night of firefighting

## Improving On-Call

### Metrics to Track

**Monitor:**
- Number of pages
- Response time
- Resolution time
- Escalations
- False positives
- Burnout indicators

### Continuous Improvement

**After each rotation:**
- What went well?
- What was painful?
- What can be automated?
- What needs documentation?
- What requires training?

**Iterate on:**
- Runbooks
- Monitoring
- Alerting
- Tools
- Process

### Alert Quality

**Good alerts:**
- Actionable (can do something)
- Customer-impacting (matters)
- Clear (know what's wrong)
- Documented (runbook exists)

**Bad alerts:**
- False positives
- Noisy
- Unclear
- No runbook
- Not actionable

**Goal:** Only alert on things that need human response NOW.

## Burnout Prevention

### Warning Signs

- Dreading rotation
- Health issues
- Constant fatigue
- Resentment
- Declining performance

### Prevention

**Sustainable practices:**
- Adequate team size (4+ engineers minimum)
- Fair compensation
- Reasonable expectations
- Recovery time
- Shared responsibility

**If unsustainable:**
- Hire more engineers
- Reduce on-call frequency
- Improve systems reliability
- Better monitoring/automation

**See [Burnout Prevention](../heuristics/burnout-prevention.md)**

## Common Issues

**Too many pages:**
- Fix root causes
- Better alerting
- Automation

**Poor documentation:**
- Runbook review
- Update after incidents
- Make it a priority

**Unfair rotation:**
- Some people always volunteering
- Others never participating
- Enforce fairness

**No compensation:**
- Advocate for budget
- Time-in-lieu alternative
- Recognition at minimum

## Resources

- [ ] "Site Reliability Engineering" by Google
- [ ] PagerDuty On-Call Guide
- [ ] "The Phoenix Project" by Gene Kim

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

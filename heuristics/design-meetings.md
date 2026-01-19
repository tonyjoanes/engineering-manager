# Design Meeting Participation

A framework for actively participating in design discussions and technical reviews.

## The Core Questions Framework

When participating in design meetings, structure your thinking around these key questions:

### 1. **Keyword Capture**
- Take notes of important terms, concepts, and decisions
- Track technical terminology and new concepts introduced
- Note action items and open questions
- Record assumptions being made

### 2. **Who Does This Affect?**
Consider the stakeholders and impacted parties:
- Which teams will need to integrate with this?
- Which users/customers will experience this change?
- Who needs to be notified about this change?
- Which downstream systems depend on this?
- Who will maintain this code long-term?

### 3. **How Will This Scale?**
Think about growth and edge cases:
- What happens at 10x the current load?
- What happens at 100x?
- Are there bottlenecks in the design?
- How does this handle peak traffic vs normal traffic?
- What are the resource implications (CPU, memory, storage, network)?
- Does this design support horizontal scaling?

### 4. **Who Is Affected If It Breaks?**
Consider the failure modes and blast radius:
- What's the impact if this service goes down?
- Which critical paths depend on this?
- Is there a single point of failure?
- What's the degradation strategy?
- How do we detect when it's broken?
- What's the rollback strategy?
- Are there cascading failure risks?

## During the Meeting

### Active Listening
- Don't just wait for your turn to speak
- Build on others' ideas
- Ask clarifying questions early

### Question Types to Use
- **Clarifying**: "When you say X, do you mean...?"
- **Scaling**: "How does this handle...?"
- **Risk**: "What happens if...?"
- **Alternatives**: "Have we considered...?"
- **Dependencies**: "What does this require from...?"

### Red Flags to Watch For
- Vague success metrics
- Unclear ownership
- Missing monitoring/observability plans
- No rollback strategy
- Unstated assumptions
- "We'll figure it out later" for critical components

## After the Meeting

- [ ] Review your keyword notes
- [ ] Verify all action items have owners
- [ ] Document decisions and rationale
- [ ] Follow up on open questions
- [ ] Share notes with relevant stakeholders

## Example Template

Use this mental checklist during discussions:

```
Design: [Name of proposed change]

Keywords/Concepts:
-

Affected parties:
- Teams:
- Users:
- Systems:

Scaling considerations:
- Current load:
- Expected growth:
- Bottlenecks:

Failure impact:
- Blast radius:
- Dependencies:
- Mitigation:
```

---

[← Back to Heuristics](./README.md) | [← Back to Index](../README.md)

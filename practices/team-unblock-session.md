# Team Unblock Session (60 Minutes)

The team version of the [High-Output 1:1](../leadership/high-output-one-on-ones.md). It uses the same five phases, applied to the whole team, to surface load, remove shared friction, agree the one thing that unlocks the most, finish it together, and get feedback on how you're leading.

> **Source:** adapted from a "60-minute 1:1" framework by @thecareerbloom (Instagram), extended here for teams.

## When to Use It

| Good fit | Use something else |
|----------|--------------------|
| The team feels busy but nothing seems to finish | Reflecting on a completed sprint → [Retrospective](./retrospectives.md) |
| Several people raise the same friction in 1:1s | After an incident → [post-incident review](./incident-management.md) |
| Too many priorities in flight, unclear focus | Planning next quarter → [Planning & Prioritization](./planning-prioritization.md) |
| Mid-sprint or mid-quarter reset | Deep interpersonal conflict → [Conflict Resolution](../leadership/conflict-resolution.md) |

**Rhythm:** monthly, or whenever the team feels stuck. It pairs well with retros on alternate fortnights.

**Size:** works best with 3-9 people. For larger groups, split into breakouts for the Friction Audit.

## At a Glance

```
00 ─ 05   Load Check        How full is everyone's plate?
05 ─ 20   Friction Audit    What's slowing us down, and who removes it?
20 ─ 30   Lead Domino       Which one thing, done, unlocks the most?
30 ─ 50   Swarm Block       Let's move it forward together, now
50 ─ 60   Power Flip        What should I (and we) do differently?
```

---

## Before the Session

- [ ] Gather friction themes you've heard in recent 1:1s (anonymised)
- [ ] Pull light data, e.g. work in progress, blocked items, PR wait times, [DORA trends](./developer-productivity-metrics.md)
- [ ] Set up a shared board (Miro, FigJam, whiteboard, or a doc)
- [ ] Tell the team the purpose: *"An hour to actually unblock ourselves, not another status meeting."*

---

## 00-05m: Load Check

**Script:**
> "Before we dive in: on a scale of 1-5, how full does your plate feel right now? Just the number. You don't need to explain it."

- Use a **fist-of-five** or an anonymous poll for honesty
- Look at the spread, not the individuals. Several 5s means a capacity conversation
- Follow up privately with anyone at 5. Don't put them on the spot

---

## 05-20m: Friction Audit

**Script:**
> "Thinking about the last couple of weeks: where did we get stuck? What process, dependency, tool or hand-off is the biggest bottleneck for us as a team?"

**Format (1-2-4-All works well):**
1. **2 min silent writing:** one friction per sticky note
2. **5 min:** cluster similar items
3. **3 min:** dot-vote, three dots each
4. **5 min:** sort the top items into buckets

| Bucket | Owner | Example |
|--------|-------|---------|
| **Manager removes** | You | Escalate a cross-team dependency, fix an approval process |
| **Team removes** | A named team member | Fix the flaky test suite, update the runbook |
| **Raise externally** | You + platform / other team | Pipeline speed, environment access, [Team Topologies](./team-topologies.md) interaction mode |
| **Accept for now** | Nobody | Named and parked so it stops draining energy |

**Guidance:**
- Talk about systems and hand-offs, never "person X is slow"
- Every item gets an owner and a date, or explicitly goes to "accept for now"

---

## 20-30m: Lead Domino

**Script:**
> "Out of everything in flight, which one piece of work, once done, would make the most other things easier or unnecessary? For the rest of this week, that's our focus."

**Helpful questions:**
- "What's blocking the most other work?"
- "What's been 'nearly done' the longest?"
- "What could we stop or pause to make room?"

**Make it real:**
- Define "done" and a date
- Agree what pauses. Say it out loud and tell stakeholders. See [Saying No](../heuristics/saying-no.md)
- Limit work in progress until it's done

---

## 30-50m: Swarm Block

**Script:**
> "Let's stop talking about it and start doing it. For the next 20 minutes, everyone works on the lead domino together."

**Options:**
- **Mob session:** one driver, everyone navigates, rotate every few minutes
- **Split and swarm:** break the domino into chunks, pairs take one each, regroup at 45m
- **Decision sprint:** if the domino is stuck on a decision, make it now and record it as an ADR
- **Review blitz:** clear the PR / review queue blocking the domino

**Guidance:**
- The manager facilitates and removes blockers live. The manager doesn't drive
- If the domino can't be worked on in the room, swarm on the top "team removes" friction instead
- Finish with a two-minute check: what's done, what's next, who has it

---

## 50-60m: Power Flip

**Script:**
> "I want to make sure I'm helping this team, not getting in its way. What did I do, or not do, recently that slowed us down? And what should I start, stop or keep doing?"

**Make it safe:**
- Collect it **anonymously** (form, sticky notes, poll) for the first few sessions
- Respond like you would in a 1:1: thank people, don't defend, pick one action, report back next time
- Optionally flip it to the team too: "What's one thing *we* should change about how we work together?"

See [Psychological Safety](./psychological-safety.md).

---

## Close and Follow-Up

**Last minute, out loud:**
- Lead domino, done-definition, date
- Friction actions with owners
- Your Power Flip commitment

**Within 24 hours:**
- [ ] Post the summary in the team channel or wiki
- [ ] Tell stakeholders what's paused
- [ ] Start on your manager-owned friction items

**Next session:**
- [ ] Open by reviewing last time's actions. Visible follow-through is what keeps people engaged

## Summary Template

```markdown
# Team Unblock Session - [Team] - [Date]

## Load Check
- Spread: [e.g. 1×2, 3×3, 2×4, 1×5]
- Follow-ups: [private check-ins needed]

## Friction
| Friction | Votes | Bucket | Owner | By |
|----------|-------|--------|-------|----|

## Lead Domino
- Task:
- Done looks like:
- By:
- Paused until then:

## Swarm Outcome
- Progress:
- Next steps / owner:

## Power Flip
- Feedback for manager:
- What I'll change:
- Team change we agreed:
```

## Anti-Patterns

### ❌ Status round-robin
"Let's go round and everyone says what they're working on" is not a friction audit.

### ❌ Friction without follow-through
Running this twice without visible change teaches the team that raising issues is pointless.

### ❌ Manager drives the swarm
You become the bottleneck you were trying to remove.

### ❌ Every domino is the manager's priority
If the team never picks its own domino, ask why.

### ❌ Public Power Flip too early
In low-trust teams, collect feedback anonymously until it's safe to do it openly.

## Related Guides

- [High-Output 1:1](../leadership/high-output-one-on-ones.md): the individual version
- [Retrospectives](./retrospectives.md)
- [Team Health Metrics](./team-health-metrics.md)
- [Psychological Safety](./psychological-safety.md)
- [Capacity Planning & Scheduling](./capacity-planning-scheduling.md)
- [Prompt: Team Unblock Session Design](../prompt-bank/team-prompts.md#team-unblock-session-design)

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

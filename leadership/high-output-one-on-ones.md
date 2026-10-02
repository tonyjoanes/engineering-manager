# The High-Output 1:1 (60-Minute Framework)

A structured 60-minute 1:1 that moves past status updates. In one hour you surface what's weighing on someone, remove what's slowing them down, finish something real together, and get honest feedback on how you're doing as their manager.

> **Source:** adapted from a "60-minute 1:1" framework shared by @thecareerbloom (Instagram). The phases below keep the original structure. The scripts, guidance and variations have been reworked for engineering teams.

## When to Use It

This format **adds to** your regular [1:1s](./one-on-ones.md). It doesn't replace them.

| Use it when... | Stick with a standard 30-min 1:1 when... |
|----------------|------------------------------------------|
| Someone is stuck, overloaded or losing momentum | Things are flowing and they have their own agenda |
| Work keeps slipping to "I'll look at it later" | The person mainly needs space to talk |
| You haven't asked for feedback on yourself in a while | It's a career, performance or personal conversation (use the dedicated guides) |
| Monthly, as a deeper session alongside weekly 30-min 1:1s | You can't protect a full hour without interruptions |

**Suggested rhythm:** weekly 30-min 1:1 + one 60-min high-output session a month (or on demand).

## The Five Phases at a Glance

```
00 ─ 05   Context Shift     What's taking up your headspace?
05 ─ 20   Friction Audit    Where did you get stuck, and on who or what?
20 ─ 30   Lead Domino       Which one task makes the rest easier?
30 ─ 50   Co-Working Block  Let's move that task forward together, now
50 ─ 60   Power Flip        What should I be doing differently?
```

> **Change from the original:** the original runs Co-Working (20-45) *before* Lead Domino (45-55). We swap them. Pick the domino first, then use the co-working time on it, so the hands-on time goes to the task that matters most. The Power Flip also gets 10 minutes instead of 5, because that slot is usually the first thing an overrunning meeting cuts.

---

## Before the Meeting (5 minutes)

- [ ] Tell them the format in advance so the co-working block isn't a surprise: *"Next week let's do a longer session. Bring one thing you'd like to get over the line together."*
- [ ] Check last session's actions. Did *you* do yours?
- [ ] Look at what they're working on: board, PRs, docs. Do this to understand the context, not to audit them.
- [ ] Block the full hour. Notifications off.
- [ ] Have the shared 1:1 doc open (template [below](#notes-template)).

---

## 00-05m: The Context Shift

**Purpose:** get past pleasantries and find out what's taking up their mental bandwidth, so you catch overwhelm before it becomes [burnout](../heuristics/burnout-prevention.md).

**Script:**
> "I want this hour to go on what actually matters to you. Setting the project list aside for a second, what's taking up the most space in your head right now? Work or not work, share as much or as little as you like."

**Alternatives if that feels too heavy:**
- "On a scale of 1-10, how full is your plate right now? What would make it a 7?"
- "What's the thing you keep thinking about after you log off?"
- "If you could make one worry disappear this week, which would it be?"

**Guidance:**
- **Offer, don't push.** "Nothing major" is a valid answer. Don't dig unless they open the door.
- **Listen, don't fix yet.** Reflect it back: "So the migration deadline is the thing looming."
- **Watch for signals:** short answers, mentions of sleep, the same worry several weeks running.
- **Escalate gently** if it's personal or serious: pause the framework and switch to a [support conversation](../prompt-bank/one-on-one-prompts.md#burnout-check-in-11). The framework can wait.

---

## 05-20m: The Friction Audit

**Purpose:** find the "sand in the gears" (the people, processes and tools slowing them down) and turn it into actions with an owner.

**Script:**
> "Thinking about the last week or two, where did you feel stuck or slowed down? What or who is the biggest bottleneck to your progress right now?"

**Probe across four areas:**

| Area | Prompt |
|------|--------|
| **Process** | "Was there anything you were waiting on: approvals, reviews, environments?" |
| **People** | "Is there anyone you need something from and aren't getting it?" |
| **Tools / platform** | "What slowed you down technically: builds, pipelines, access, flaky tests?" |
| **Clarity** | "Is there anything where you're not sure what 'done' looks like, or who decides?" |

**Then sort each item:**

| Bucket | Who acts | Example |
|--------|----------|---------|
| **I'll remove it** | Manager | Chase the approval, escalate the dependency, get the access |
| **You can remove it** | Them, with your backing | "You have my support to push back on that request" |
| **We need to raise it** | Team / platform | Add to retro, platform backlog, or [capacity planning](../practices/capacity-planning-scheduling.md) |
| **We accept it for now** | Nobody, for now | Name it so it stops draining energy |

**Guidance:**
- **Focus on systems, not blame.** If a person is the bottleneck, talk about the hand-off, not the person's character. Use [conflict resolution](./conflict-resolution.md) if it's a real interpersonal problem.
- **Patterns matter.** The same friction from three people is a team or platform problem. Take it to the [team version](../practices/team-unblock-session.md) or a [retro](../practices/retrospectives.md).
- **Write down every "I'll remove it" item.** Doing those is how they learn whether this meeting is worth it.

---

## 20-30m: The Lead Domino

**Purpose:** apply the Pareto principle to their list. Find the one task that, once done, makes the rest easier or unnecessary.

**Script:**
> "We've touched on a few priorities. Out of everything on your plate, which one is the lead domino, the task that would make the others easier, or even unnecessary, once it's done? Let's agree to treat everything else as noise until that one's done."

**Helpful questions if they're unsure:**
- "What's blocking the most other things, or other people?"
- "Which one, if it slipped another week, would hurt most?"
- "Which one are you avoiding? Why?"
- "What could we stop doing entirely?"

**Guidance:**
- **They choose; you sanity-check.** If their domino conflicts with team priorities, say so openly and agree together.
- **Give them cover.** "Ignore the noise" only works if you protect them from it: "If anyone asks about X this week, point them to me."
- **Make it concrete:** what does "done" look like, and by when?
- See [Saying No](../heuristics/saying-no.md) and [Planning & Prioritization](../practices/planning-prioritization.md) for the "what to drop" conversation.

---

## 30-50m: The Co-Working Block

**Purpose:** stop talking about the work and do some of it together. Move the lead domino from "I'll look at it later" to "it's moved forward, or done, now".

**Script:**
> "Let's switch from the 'what' to the 'how'. Pull up the draft, deck or code for that task and let's spend the next 20 minutes on it together. What's the best use of this time: reviewing, untangling a problem, or making a decision?"

**Good uses of the block:**
- Reviewing a design doc, PR, ADR or proposal and agreeing changes live
- Untangling a technical problem together (debugging, design trade-off)
- Drafting the hard email or message to a stakeholder
- Making a decision they've been waiting on you for
- Breaking a big, scary task into small first steps
- Rehearsing a presentation or difficult conversation

**Guidance:**
- **They drive, you navigate.** They share their screen and type. The moment you take the keyboard, it becomes your work, not their growth. See [Delegation](./delegation.md).
- **Coach before you tell.** Ask "What options have you considered?" before suggesting. Use [GROW](./grow-model.md) if they're stuck.
- **Unblock, don't take over.** If the fix is "you need my approval", give it in the room.
- **It's OK to skip.** If nothing needs hands-on time, give the time back or go deeper on friction or growth. Don't invent work to fill the slot.
- **Senior engineers:** turn it into a thinking-partner session on strategy, influence or a design they own.

---

## 50-60m: The Power Flip

**Purpose:** ask for honest feedback on *your* performance as their manager. This is the part that builds trust over time.

**Script:**
> "I want to make sure I'm helping you, not holding you back. Honestly: what did I do, or not do, recently that slowed you down or frustrated you?"

**Why this phrasing works:** it assumes there *is* something, which makes it easier to answer than "Any feedback for me?" (which almost always gets "No, all good").

**Alternatives to rotate:**
- "What's one thing I should start, stop or keep doing?"
- "Where would you like more support from me, or less involvement?"
- "If you were managing you, what would you do differently from me?"
- "What's something you think I don't know about how the team is feeling?"

**How to respond, which matters more than the question:**
1. **Thank them.** "Thank you, that's useful."
2. **Don't defend or explain.** Not even a little.
3. **Clarify if needed.** "Can you give me an example so I get it right?"
4. **Commit to one action** and write it in the shared doc.
5. **Close the loop** at the next 1:1: "Last time you said X. Here's what I've changed. Is it better?"

**Guidance:**
- **Expect silence at first.** Trust builds over several sessions. Keep asking.
- **Model it.** Share something you're working on improving yourself.
- **Never punish candour.** One defensive reaction resets the trust to zero. See [Psychological Safety](../practices/psychological-safety.md).

---

## Close (last 60 seconds)

Summarise out loud:
- **Their lead domino** and what "done" means
- **Your actions** (friction you'll remove + your Power Flip commitment)
- **Their actions**
- **When you'll check in**

---

## Notes Template

```markdown
# High-Output 1:1 - [Name] - [Date]

## Context Shift
- On their mind:
- Signals to watch:

## Friction Audit
| Friction | Bucket (I'll remove / You remove / Raise / Accept) | Owner | By |
|----------|---------------------------------------------------|-------|----|
|          |                                                   |       |    |

## Lead Domino
- Task:
- Done looks like:
- By:
- Noise we're ignoring until then:

## Co-Working
- What we worked on:
- Outcome / decisions:

## Power Flip
- Feedback for me:
- What I'll change:

## Follow-up
- [ ] Manager actions
- [ ] Their actions
- [ ] Check-in date
```

---

## 30-Minute Version

When you can't get an hour, keep all five phases and compress them:

| Time | Phase | Change |
|------|-------|--------|
| 0-3 | Context Shift | One question only |
| 3-10 | Friction Audit | Top one or two frictions only |
| 10-14 | Lead Domino | Pick it, define done |
| 14-25 | Co-Working | One focused decision or review |
| 25-30 | Power Flip | One question, one commitment |

---

## Adapting for Different People

| Person | Adjust |
|--------|--------|
| **New starter** | Make the Friction Audit about onboarding gaps; use co-working to pair on their first real task. See [Onboarding](./onboarding.md) |
| **Senior / staff engineer** | Lighter on tasks, heavier on organisational friction and influence; co-working becomes thinking-partner time |
| **Struggling performer** | Use the Lead Domino to create focus and early wins; keep it supportive, not a disguised review. See [Underperformance](./underperformance.md) |
| **High performer** | Friction Audit often uncovers being over-used; check the Lead Domino isn't everyone else's priority |
| **Remote** | Cameras on if they're comfortable; use a shared doc throughout; co-working on screen-share works well |
| **Introvert / reflective** | Send the questions in advance so they can think them through |

---

## Anti-Patterns

### ❌ Turning it into a status meeting
If you catch yourself asking "where are we with X?", stop. Status belongs in async updates or stand-up.

### ❌ Taking over the co-working block
Rewriting their doc or code yourself helps for a day and hurts their growth for months.

### ❌ Forcing the Context Shift
Pushing for personal disclosure feels intrusive. Offer the door; let them choose to walk through it.

### ❌ Skipping the Power Flip because you ran out of time
It's the most valuable 10 minutes. Protect it, and cut the co-working block short if you have to.

### ❌ Collecting friction and doing nothing
After two sessions with no visible action on their friction, people stop bringing it up.

### ❌ Running every 1:1 like this
It's intense. Mix it with lighter 1:1s that the other person leads.

---

## Related Guides

- [One-on-One Meetings](./one-on-ones.md): the regular 1:1 foundation
- [Team Unblock Session](../practices/team-unblock-session.md): the team version of this framework
- [GROW Model](./grow-model.md): coaching during the co-working block
- [Feedback Models](./feedback-models.md): giving and receiving feedback
- [Delegation](./delegation.md): staying in the navigator seat
- [Burnout Prevention](../heuristics/burnout-prevention.md): acting on Context Shift signals
- [Prompt: High-Output 1:1 Preparation](../prompt-bank/one-on-one-prompts.md#high-output-11-preparation)

---

[← Back to Leadership](./README.md) | [← Back to Index](../README.md)

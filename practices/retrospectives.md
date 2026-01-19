# Team Retrospectives

Running effective retrospectives that drive continuous improvement.

## What is a Retrospective?

**Definition:** A regular meeting where the team reflects on how they work and identifies improvements.

**Purpose:**
- Inspect and adapt
- Continuous improvement
- Team ownership of process
- Build psychological safety
- Celebrate wins

**When to hold:**
- End of each sprint (Scrum)
- After major projects
- Monthly (if not doing sprints)
- After incidents
- When team requests

**Duration:** 60-90 minutes for 2-week sprint

## Why Retrospectives Matter

**With good retros:**
- Team continuously improves
- Issues surface and get resolved
- Everyone has voice
- Process evolves with needs
- Team ownership and engagement

**Without retros:**
- Same problems repeat
- Frustrations build
- Process becomes rigid
- Disengagement grows
- Stagnation

**The most important meeting for team health.**

## The Basic Format

### Standard Structure (60 min)

**1. Set the Stage (5 min)**
- Welcome and purpose
- Review ground rules
- Check-in or ice breaker

**2. Gather Data (15 min)**
- What happened this sprint?
- Collect facts and feelings
- Everyone contributes

**3. Generate Insights (15 min)**
- Why did things happen?
- What patterns do we see?
- What's the root cause?

**4. Decide What to Do (20 min)**
- What will we try?
- Who owns it?
- How will we measure?

**5. Close (5 min)**
- Summarize actions
- Appreciate contributions
- Feedback on retro itself

## Setting the Stage

### Prime Directive

**Read this at the start:**

> "Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand."

**Why it matters:**
- Sets tone of psychological safety
- Focuses on learning, not blame
- Assumes positive intent

### Ground Rules

**Typical agreements:**
- Vegas rule (what's said here, stays here)
- One conversation at a time
- Assume positive intent
- Focus on what we can control
- Be honest and respectful
- No devices (phones away)

### Check-In Activity

**Quick engagement:**
- "Rate your sprint 1-5, one word why"
- "One word to describe how you're feeling"
- "What's on your mind?"
- "Energy level check"

**Helps people:**
- Transition into the meeting
- Surface emotional state
- Warm up for sharing

## Gathering Data

### Classic Format: Start/Stop/Continue

**Three columns:**

**START** - What should we begin doing?
- Example: "Start having design reviews before coding"
- Example: "Start using feature flags"

**STOP** - What should we quit doing?
- Example: "Stop scheduling meetings during deep work hours"
- Example: "Stop skipping code reviews when rushed"

**CONTINUE** - What's working?
- Example: "Continue pair programming on complex features"
- Example: "Continue team lunches"

**Process:**
- 5 minutes: Everyone writes sticky notes (silent)
- 10 minutes: Take turns sharing and clustering

### Alternative: Mad/Sad/Glad

**Three emotions:**

**MAD** - What frustrated you?
**SAD** - What disappointed you?
**GLAD** - What made you happy?

**Good for:**
- Surfacing emotions
- Psychological safety
- Understanding morale

### Alternative: 4 Ls

**LIKED** - What went well?
**LEARNED** - What did we discover?
**LACKED** - What was missing?
**LONGED FOR** - What do we wish we had?

**Good for:**
- Growth mindset
- Positive framing
- Forward-looking

### Alternative: Sailboat

**Visual metaphor:**

**Island (Goal):** Where we're trying to go
**Wind (Helps):** What's pushing us forward
**Anchor (Hinders):** What's holding us back
**Rocks (Risks):** What could sink us

**Good for:**
- Visual thinkers
- Understanding blockers
- Seeing progress toward goals

### Alternative: Timeline

**Draw the sprint:**
- X-axis: Time (Day 1 to Day 10)
- Y-axis: Mood (Happy to Sad)
- Everyone plots high and low points

**Good for:**
- Seeing patterns
- Understanding emotions
- Identifying specific moments

### Tips for Data Gathering

**Ensure everyone participates:**
- Silent writing first (no groupthink)
- One item per sticky note
- Read your own sticky notes
- No interrupting while sharing

**Cluster similar items:**
- Group related themes
- Name the clusters
- Count votes if needed

**Make it visual:**
- Use physical or virtual board
- Color-coding
- Sticky notes or digital tools

## Generating Insights

### Five Whys

**Dig deeper into root causes:**

**Example:**
- Problem: "Deployments are slow"
- Why? "Tests take forever"
- Why? "We have too many integration tests"
- Why? "We don't trust unit tests"
- Why? "Unit tests miss things"
- Why? "We don't write comprehensive unit tests"
- Root cause: Test writing practices

**Use sparingly** - Can feel interrogative

### Fishbone Diagram (Ishikawa)

**For complex problems:**

```
          People      Process      Technology
             |            |              |
             ↓            ↓              ↓
        ──────────────Problem────────────────
             ↑            ↑              ↑
             |            |              |
         Methods     Environment    Materials
```

**Identify contributing factors in each category**

### Dot Voting

**Prioritize what to discuss:**
- Each person gets 3-5 votes
- Place dots on items most important to them
- Discuss highest-voted items

**Ensures:**
- Democratic prioritization
- Focus on what matters most
- Time used wisely

### Discussion

**Guide the conversation:**
- What's the root cause?
- Why is this happening?
- What patterns do we see?
- Is this a one-time thing or recurring?
- What's within our control?

**Keep it productive:**
- Focus on team's sphere of influence
- Don't dwell on things we can't change
- Look for systemic issues, not individuals
- Turn complaints into actionable insights

## Deciding What to Do

### Action Item Criteria

**Good action items are:**

**SMART:**
- **Specific:** Clear what to do
- **Measurable:** Can tell if done
- **Achievable:** Realistic
- **Relevant:** Addresses root cause
- **Time-bound:** When by (usually next sprint)

**Examples:**

❌ Bad: "Improve communication"
✓ Good: "Start 15-min daily standup at 10am, Jamie facilitates"

❌ Bad: "Better code reviews"
✓ Good: "All PRs reviewed within 24 hours. If not, @ reviewer in Slack - Alex will track this week"

❌ Bad: "Be more productive"
✓ Good: "Block Tue/Thu afternoons for deep work (no meetings), manager enforces"

### Limit Action Items

**Don't try to fix everything:**
- 1-3 action items per retro
- Focus on highest impact
- Complete previous actions first
- Better to finish 2 than start 10

**The graveyard of incomplete retro actions is full.**

### Assign Owners

**Every action needs:**
- Clear owner (specific person)
- Due date (usually next retro)
- Definition of done

**Example:**
```
Action: Start writing architecture decision records (ADRs)
Owner: Jordan
By: Next retro
Definition of done: Template created, first 3 decisions documented, shared with team
```

### Types of Actions

**Process changes:**
- "Change standup to async Slack thread"
- "Add 'what did we learn?' to incident post-mortems"

**Experiments:**
- "Try pairing on all features this sprint"
- "Experiment with no-meeting Wednesdays"

**Tools or resources:**
- "Set up staging environment"
- "Get licenses for [tool]"

**Learning:**
- "Do lunch & learn on [topic]"
- "Create doc on [process]"

**Celebrations:**
- "Team lunch to celebrate launch"
- "Recognize [person] for [contribution]"

### Follow Up on Previous Actions

**Start each retro with:**
- Review previous action items
- Did we do them?
- Did they work?
- Continue, adjust, or stop?

**If incomplete:**
- Why not?
- Still important?
- New owner or drop it?

**Accountability:**
- Track completion rate
- If always incomplete, too many or not important

## Closing the Retro

### Summarize

**Quick recap:**
- Key insights
- Action items and owners
- Appreciations
- Next steps

**Send follow-up:**
- Email or doc with notes
- Action items prominently listed
- Share with team and stakeholders

### Plus/Delta on the Retro

**Meta-retrospective:**
- What worked well about this retro?
- What could we change for next time?

**Continuous improvement applies to retros too!**

### Appreciations

**End on positive note:**
- Thank people for contributions
- Shout out good work
- Recognize helpfulness
- Build team cohesion

**Formats:**
- "I appreciated when [person] did [thing]"
- Go around circle
- Sticky notes of appreciation
- Kudos in Slack channel

## Retrospective Variations

### After Major Projects

**Longer format (2 hours):**
- Bigger scope (whole project, not just sprint)
- More participants (all contributors)
- Deeper analysis
- Document for future projects

**Questions:**
- What went well?
- What was challenging?
- What would we do differently?
- What did we learn?
- What should other teams know?

### Futurespective

**Instead of looking back, look forward:**
- Imagine project is done and successful
- What did we do to make it successful?
- What obstacles did we overcome?
- How did we work together?

**Use for:**
- Project kickoffs
- Team planning
- Vision setting

### Team Health Check

**Periodic deep dive:**
- Not sprint-focused
- Team dynamics and satisfaction
- Career goals and growth
- Work-life balance
- Long-term improvements

**Use:**
- Quarterly
- When team is struggling
- New team formation

### Silent Retro

**All written, no talking:**
- Use shared doc or board
- Everyone writes simultaneously
- Comment on each other's items in writing
- Vote on actions
- Read out actions at end

**Good for:**
- Remote teams
- Equal participation
- Detailed thoughts
- Avoiding groupthink

### Walking Retro

**Get moving:**
- Walk outside (weather permitting)
- Small groups (3-4 people)
- Casual discussion
- Return and share insights

**Good for:**
- Team energy boost
- Different environment
- Informal tone
- Nice weather days

## Remote Retrospectives

### Tools

**Virtual boards:**
- Miro
- Mural
- Retrium
- FunRetro
- EasyRetro

**Features to use:**
- Timer for activities
- Anonymous submission
- Voting
- Grouping/clustering
- Templates

### Remote-Specific Practices

**Engage camera-off folks:**
- Have everyone type in chat
- Use polls
- Breakout rooms for small groups
- Anonymous submissions

**Combat Zoom fatigue:**
- Keep it 45-60 min max
- More async prep work
- Interactive activities
- Breaks if needed

**Ensure participation:**
- Call on people specifically
- "Let's hear from people who haven't shared"
- Mix individual and group activities

## Common Retrospective Problems

### Problem: Same Issues Every Time

**Why:**
- Not following through on actions
- Root causes not addressed
- Outside team's control

**Solutions:**
- Review action completion
- Dig deeper with Five Whys
- Escalate issues outside control
- Experiment with different solutions

### Problem: People Don't Speak Up

**Why:**
- Lack of psychological safety
- Dominant voices
- Fear of retaliation
- Don't see point

**Solutions:**
- Anonymous input
- Silent writing first
- Break into smaller groups
- One-on-one before retro
- Address safety issues
- Show actions being taken

### Problem: Manager Dominates

**Why:**
- Manager talks too much
- Defensive about criticism
- Problem-solving instead of facilitating

**Solutions:**
- Have someone else facilitate
- Manager speaks last
- Manager leaves for part of retro
- Manager just listens

### Problem: Retro Feels Like Waste of Time

**Why:**
- No actions taken
- Same format every time
- Going through motions
- Not addressing real issues

**Solutions:**
- Skip retro if no topics (rare)
- Vary the format
- Make action completion visible
- Have meta-retro on making retros better

### Problem: Turns into Blame Session

**Why:**
- Psychological safety lacking
- Finger-pointing
- Personal attacks
- Revisiting past grievances

**Solutions:**
- Restate Prime Directive
- Redirect to systemic issues
- "What could we change to prevent this?"
- Facilitate neutrally
- Address toxic behavior offline

### Problem: Only Negative

**Why:**
- Culture of complaint
- Not celebrating wins
- Focusing only on problems

**Solutions:**
- Start with appreciations
- Require "what went well" section
- Celebrate small wins
- Balance problem-solving with recognition

## Facilitating Great Retros

### The Facilitator's Role

**Prepare:**
- Gather data beforehand
- Choose format
- Set up space/tools
- Review previous actions

**During:**
- Keep time
- Ensure everyone participates
- Redirect if off-track
- Capture notes
- Stay neutral

**After:**
- Send notes
- Track action items
- Follow up on completion

### Facilitation Tips

**Timebox activities:**
- Use visible timer
- Warn at 2 minutes left
- Move on when time's up (can return if time)

**Encourage quieter people:**
- "Let's hear from [name]"
- Round-robin formats
- Written before verbal
- Break into pairs first

**Handle difficult moments:**
- Conflict → "Let's discuss offline"
- Off-topic → "Parking lot for later"
- Dominant person → "Let's hear other perspectives"
- Emotional → Pause, acknowledge, continue

**Stay neutral:**
- Don't problem-solve
- Don't defend
- Don't take sides
- Facilitate, don't participate

### Rotating Facilitation

**Benefits:**
- Everyone learns skill
- Shared ownership
- Manager not always in charge
- Fresh perspectives

**How:**
- Volunteer or rotate alphabetically
- Provide facilitation guide
- Debrief after
- Manager facilitates occasionally, not always

## Making Retros Engaging

### Mix Up Formats

**Don't do same format every time:**
- Use different templates
- Try new activities
- Vote on which format
- Create your own

**Rotation example:**
- Sprint 1: Mad/Sad/Glad
- Sprint 2: Timeline
- Sprint 3: 4Ls
- Sprint 4: Team's choice

### Use Creativity

**Beyond sticky notes:**
- Draw instead of write
- LEGO building
- Superhero metaphors
- Movie poster of sprint
- Weather report

**Energize:**
- Music during writing
- Physical movement
- Gamification
- Competitions (healthily)

### Make It Fun

**Doesn't have to be serious:**
- Humor welcome
- Inside jokes
- Celebrations
- Treats/snacks
- Fun virtual backgrounds (remote)

**Balance:** Fun AND productive

## Measuring Retro Effectiveness

### Good Signs

✓ High participation
✓ Psychological safety evident
✓ Action items getting completed
✓ Real issues being raised
✓ Team ownership of process
✓ Visible improvements over time
✓ Team asks for retros

### Bad Signs

✗ People skip retros
✗ Silence or superficial sharing
✗ No actions or incomplete actions
✗ Same problems every retro
✗ Complaints but no solutions
✗ Manager does all talking
✗ "Waste of time" sentiment

### Track Over Time

**Monitor:**
- Action completion rate
- Topics raised (are they substantial?)
- Participation (who speaks?)
- Improvements shipped
- Team satisfaction with retros

**Quarterly review:**
- Are retros working?
- What should we change?
- Do we need more/fewer?

## Advanced Techniques

### Lean Coffee Format

**No agenda, emergent:**
- Generate topics
- Vote on topics
- Time-box discussions (5-10 min)
- Vote to continue or move on
- Democratic and adaptive

### Delegation Poker

**For action items:**
- Decide delegation level (1-7)
- How much autonomy does owner have?
- Clear authority and accountability

### Solution Tree

**For complex problems:**
- Define problem
- Brainstorm solutions
- Map solutions to root causes
- Prioritize high-impact solutions

### Force Field Analysis

**Identify:**
- Driving forces (helping)
- Restraining forces (hindering)
- Strengthen drivers
- Reduce restraints

## Resources

- [ ] "Agile Retrospectives" by Esther Derby & Diana Larsen
- [ ] "The Retrospective Handbook" by Patrick Kua
- [ ] Retromat.org - 100+ retro activities
- [ ] Fun Retrospectives - Free retro activities
- [ ] "Project Retrospectives" by Norman Kerth

---

[← Back to Practices](./README.md) | [← Back to Index](../README.md)

# Elon Musk's 5-Step Engineering Process

A systematic approach to engineering and manufacturing that prioritizes simplification and efficiency.

## The Five Steps (In Order)

### 1. Make the Requirements Less Dumb
- **Question every requirement**, especially from smart people
- Requirements from smart people are the most dangerous because people are less likely to question them
- Everyone's wrong some of the time - requirements must come with a name, not a department
- You should be able to trace every requirement back to a specific person
- Challenge the requirement itself, not just how to implement it

**Key Questions:**
- Who made this requirement?
- What's the actual underlying need?
- Is this requirement based on outdated assumptions?

### 2. Try Very Hard to Delete the Part or Process
- If you're not occasionally adding things back in, you're not deleting enough
- The most common error is to optimize something that shouldn't exist
- Delete, delete, delete - then figure out if you deleted too much
- Every part/process should have to fight for its survival

**Key Questions:**
- What happens if we remove this entirely?
- Can we combine this with something else?
- Does this solve a real problem or an imagined one?

### 3. Simplify or Optimize
- **Only do this AFTER steps 1 and 2**
- The most common mistake: optimizing something that shouldn't exist
- Simplification can mean making it easier to understand, manufacture, or maintain
- Every part should serve a clear purpose

**Key Questions:**
- Can this be done with fewer steps?
- Can we use a simpler approach?
- Are we adding complexity to solve a problem we created?

### 4. Accelerate Cycle Time
- You're moving too slowly if you're not breaking things
- Go faster, but only after the first three steps
- Speed matters, but not at the expense of doing the wrong thing faster
- Increase iteration speed and feedback loops

**Key Questions:**
- What's the constraint on cycle time?
- Where are we waiting unnecessarily?
- Can we test/iterate faster?

### 5. Automate
- **This comes last for a reason**
- Automating a bad process just creates an automated bad process
- Only automate after the above steps are complete
- The "idiot index": cost of finished product / cost of raw materials
  - If this ratio is high, you're being an idiot (too much processing)

**Key Questions:**
- Is this process stable enough to automate?
- Will automation lock us into a suboptimal approach?
- What's the ROI of automation vs continued manual optimization?

## Why This Order Matters

Most organizations reverse this, especially steps 2 and 5:
- They automate first (most exciting)
- Then try to optimize the automated process
- They rarely delete or simplify
- They almost never question requirements

**This leads to:**
- Highly optimized processes that shouldn't exist
- Automated systems that do the wrong thing efficiently
- Complex solutions to problems nobody has

## Application Examples

### Bad Approach
1. Requirement: "We need a dashboard showing X metric"
2. Build automated pipeline for X metric
3. Optimize the dashboard performance
4. Realize nobody needs this metric

### Good Approach
1. Who needs X metric and why? (Challenge requirement)
2. Can they get this from an existing dashboard? (Delete)
3. Can we show this more simply? (Simplify)
4. Can we update it more frequently? (Accelerate)
5. Should we automate the data pipeline? (Automate)

## Common Mistakes

- **Skipping steps**: Going straight to automation
- **Wrong order**: Optimizing before simplifying
- **Not deleting enough**: "Just in case" features
- **Accepting requirements**: Not tracing back to the person
- **Moving too slow**: Not breaking things occasionally

## Related Principles

- "The best part is no part"
- "The best process is no process"
- "Optimize for deletion"
- "Make your factory smaller, not bigger"

## Sources

- Walter Isaacson's Biography
- Everyday Astronaut interview (2021)
- Various SpaceX/Tesla presentations

---

[← Back to Heuristics](./README.md) | [← Back to Index](../README.md)

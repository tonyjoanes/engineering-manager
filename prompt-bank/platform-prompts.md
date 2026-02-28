# Platform & DevOps Prompts

Ready-to-use prompts for platform engineering, DevOps, and Team Topologies scenarios.

---

## Platform Capability Decision

**When to Use:** Deciding whether to build a new platform capability or service.

**Related Resources:**
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)

**The Prompt:**
```
We're considering building a platform capability for [describe capability, e.g., "self-service database provisioning" or "golden path CI/CD templates"].

Context:
- Problem it solves: [what pain point for product teams]
- Current state: [how teams handle this today]
- Number of teams affected: [how many teams would use this]
- Frequency of need: [how often teams need this]
- Alternative solutions: [existing tools, buy vs build options]
- Platform team capacity: [current bandwidth]

Help me evaluate:
1. Is this a good platform capability? (self-service, reduces cognitive load, golden path)
2. Build vs buy vs use existing cloud service
3. Rough effort estimate and prioritization
4. Expected impact on developer experience
5. Success metrics for this capability

Reference the platform engineering guides for principles of good platform capabilities.
```

**Expected Output:**
- Build/buy/use recommendation with rationale
- Prioritization advice
- Success metrics (adoption rate, time savings, etc.)
- Implementation approach if building

**Follow-Up Actions:**
- Add to platform roadmap if building
- Pilot with one team
- Create documentation
- Measure adoption

---

## DevOps Engineer Career Development

**When to Use:** A DevOps engineer asks about career growth or what they need to do to level up.

**Related Resources:**
- [DevOps Career Ladder](../practices/devops-career-ladder.md)
- [Career Development](../leadership/career-development.md)

**The Prompt:**
```
[DevOps engineer name] wants to grow from [current level] to [target level].

Current skills and experience:
- Technical skills: [Azure, Bicep, PowerShell, pipelines, etc.]
- Years of experience: [duration]
- Current responsibilities: [what they own]
- Strengths: [list]
- Growth areas: [list]

Using the DevOps Career Ladder from my knowledge base:
1. Map their current skills to the competency matrix
2. Identify gaps between current and target level
3. Create specific development plan with milestones
4. Identify stretch opportunities in our platform work
5. Set timeline and check-in cadence

Reference the DevOps career ladder for level expectations and competency matrix.
```

**Expected Output:**
- Competency gap analysis using the career ladder
- Specific skills to develop (technical and non-technical)
- Development plan with milestones
- Stretch assignments in platform work
- Timeline to target level

**Follow-Up Actions:**
- Create written development plan
- Assign stretch work
- Regular skills assessments
- Track progress in 1:1s

---

## Team Topologies Implementation

**When to Use:** You're restructuring teams using Team Topologies principles.

**Related Resources:**
- [Team Topologies](../practices/team-topologies.md)
- [Team Topologies Anti-Patterns](../practices/team-topologies-anti-patterns.md)

**The Prompt:**
```
I want to apply Team Topologies to restructure our engineering organization.

Current state:
- Number of engineers: [total]
- Current team structure: [describe current teams]
- Pain points: [dependencies, bottlenecks, unclear ownership, etc.]
- Value streams: [customer-facing products, internal services, etc.]
- Platform capabilities: [what exists today]

Help me:
1. Identify value streams for stream-aligned teams
2. Design platform team structure and services
3. Determine if we need enabling teams
4. Map current engineers to new structure
5. Create transition plan
6. Identify anti-patterns to avoid

Reference the Team Topologies guide for the 4 team types and 3 interaction modes, and the anti-patterns guide for what to avoid.
```

**Expected Output:**
- Proposed team structure (stream-aligned, platform, enabling teams)
- Team boundaries and responsibilities
- Interaction modes between teams
- Transition plan
- Anti-pattern warnings specific to your context

**Follow-Up Actions:**
- Pilot with one stream-aligned team
- Start building platform team
- Measure dependencies
- Iterate based on feedback

---

## Platform Team Anti-Pattern Check

**When to Use:** You suspect your platform team has drifted into an anti-pattern (ticket system, bottleneck, etc.).

**Related Resources:**
- [Team Topologies Anti-Patterns](../practices/team-topologies-anti-patterns.md)
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)

**The Prompt:**
```
I'm concerned that our platform team may be in an anti-pattern.

Observable signs:
- [e.g., "teams submit tickets for deployments" or "platform team is always overwhelmed" or "teams complain about platform"]
- Platform team backlog: [growing / stable / shrinking]
- Deployment frequency: [per team, per week]
- Developer feedback: [quotes or survey results]
- Self-service adoption: [high / medium / low]

Help me:
1. Identify which anti-pattern(s) we're in (ticket system, bottleneck, etc.)
2. Diagnose root causes
3. Create course-correction plan
4. Shift to X-as-a-Service model
5. Measure improvement

Reference the Team Topologies anti-patterns guide, specifically the "Platform as a Ticket System" section.
```

**Expected Output:**
- Anti-pattern diagnosis
- Root cause analysis
- Course-correction plan with specific actions
- Metrics to track improvement
- Timeline for transformation

**Follow-Up Actions:**
- Communicate new platform model
- Build self-service capabilities
- Deprecate ticket-based workflows
- Measure adoption and satisfaction

---

## Azure Platform Design

**When to Use:** Designing a new Azure platform capability or service.

**Related Resources:**
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)
- [Azure Dev Box & Defender](../practices/azure-devbox-defender.md)

**The Prompt:**
```
We need to design a platform capability for [specific need, e.g., "web app provisioning" or "CI/CD pipelines" or "dev environments"].

Requirements:
- What teams need: [describe the use case]
- Current pain points: [manual processes, inconsistency, security gaps, etc.]
- Technology constraints: [must use Bicep / Azure DevOps / etc.]
- Security requirements: [compliance, policies, etc.]
- Scale: [number of teams, number of instances]

Design an Azure-native solution using:
1. Bicep modules (what should be parameterized vs opinionated)
2. Azure Pipeline templates (golden path)
3. PowerShell automation (if needed)
4. Azure Policy (guardrails)
5. Security built-in (Defender for Cloud)
6. Self-service experience

Reference the Azure platform engineering guide for patterns and examples.
```

**Expected Output:**
- Architecture design for the platform capability
- Bicep module structure
- Pipeline template approach
- Security and policy configuration
- Self-service workflow
- Documentation plan

**Follow-Up Actions:**
- Build POC with one team
- Create Bicep modules
- Write documentation
- Pilot and iterate
- Roll out to all teams

---

## Developer Experience Problem

**When to Use:** Product teams complain about poor developer experience or slow delivery.

**Related Resources:**
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)
- [Team Health Metrics](../practices/team-health-metrics.md)

**The Prompt:**
```
Product teams are complaining about [specific DevEx issue, e.g., "slow CI/CD pipelines" or "hard to provision infrastructure" or "too many tools to learn"].

Data:
- Specific complaints: [quotes from developers]
- DORA metrics: [deployment frequency, lead time, MTTR, change failure rate]
- Time spent on toil: [estimate percentage]
- Platform adoption: [what % use platform services]
- Recent developer survey results: [if available]

Help me:
1. Diagnose the root cause of poor DevEx
2. Prioritize which improvements would have most impact
3. Design solutions (platform capabilities, process changes, etc.)
4. Create improvement roadmap
5. Set metrics to track improvement

Reference the platform engineering & DevEx guide for DORA metrics and SPACE framework.
```

**Expected Output:**
- Root cause analysis of DevEx issues
- Prioritized improvement opportunities
- Solution approaches
- Roadmap with quick wins and longer-term improvements
- Success metrics (DORA, SPACE, satisfaction)

**Follow-Up Actions:**
- Implement quick wins first
- Build platform capabilities for bigger issues
- Measure improvement
- Resurvey developers

---

## Self-Service Capability Design

**When to Use:** You want to transform a manual/ticket-based process into self-service.

**Related Resources:**
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)
- [Team Topologies Anti-Patterns](../practices/team-topologies-anti-patterns.md) - Platform as Ticket System section

**The Prompt:**
```
We currently handle [process/request type] via tickets, and I want to make it self-service.

Current process:
- How it works today: [describe ticket-based process]
- Volume: [number of requests per week/month]
- Time to fulfill: [current turnaround time]
- Common variations: [different types of requests]
- Why it requires manual work: [approval? complex setup? lack of automation?]

Help me design a self-service solution:
1. What can be automated vs still needs human review
2. Self-service interface (CLI, portal, pipeline template, etc.)
3. Guardrails (Azure Policy, automated checks) instead of approvals
4. Documentation needed
5. Migration plan from ticket-based to self-service
6. Success metrics

Reference the Azure platform engineering guide for self-service patterns and the anti-patterns guide for avoiding platform as ticket system.
```

**Expected Output:**
- Self-service design (interface, automation, guardrails)
- What remains manual (if anything)
- Implementation plan
- Documentation outline
- Migration strategy
- Metrics (usage, success rate, time savings)

**Follow-Up Actions:**
- Build self-service capability
- Create excellent documentation
- Pilot with one team
- Deprecate ticket process
- Measure adoption

---

## Bicep Module Library Organization

**When to Use:** Setting up or reorganizing your Bicep module library for platform team.

**Related Resources:**
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)

**The Prompt:**
```
I need to design our Bicep module library structure for the platform team.

Current state:
- Existing modules: [list what you have]
- Common infrastructure patterns: [web apps, databases, functions, etc.]
- Teams using Bicep: [number and skill level]
- Azure resources we use most: [list top 10]
- Security/compliance requirements: [policies, standards]

Help me:
1. Design module library structure (registry organization)
2. Determine what should be opinionated vs parameterized
3. Versioning strategy
4. Security and compliance built into modules
5. Documentation structure
6. Consumption patterns (how teams use modules)
7. Governance (who can publish, review process)

Reference the Azure platform engineering guide for Bicep module patterns.
```

**Expected Output:**
- Module library structure and organization
- Template for common modules with security built-in
- Versioning and publishing strategy
- Documentation template
- Governance process
- Getting started guide for teams

**Follow-Up Actions:**
- Set up Azure Container Registry for modules
- Build core modules
- Create documentation site
- Onboard first team
- Iterate based on feedback

---

## DevOps vs Platform Engineering Clarity

**When to Use:** There's confusion about roles, responsibilities, or career paths between DevOps and Platform Engineering.

**Related Resources:**
- [DevOps Career Ladder](../practices/devops-career-ladder.md)
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)
- [Team Topologies](../practices/team-topologies.md)

**The Prompt:**
```
We have confusion about [DevOps engineers vs Platform engineers / DevOps team vs Platform team / career paths].

Current situation:
- Team structure: [describe current teams]
- Role definitions: [current job descriptions]
- Responsibilities: [who does what]
- Confusion points: [specific questions or conflicts]
- Company size: [number of engineers]

Help me:
1. Clarify DevOps vs Platform Engineering in our context
2. Define clear responsibilities for each
3. Determine optimal team structure (embedded DevOps + platform team, or other)
4. Create career paths for both
5. Communication plan for the organization

Reference the DevOps career ladder, Team Topologies (platform teams), and Azure platform engineering guide.
```

**Expected Output:**
- Clear definitions for your context
- Responsibility matrix (RACI)
- Recommended team structure
- Career ladder for each path
- Communication plan

**Follow-Up Actions:**
- Update job descriptions
- Communicate new structure
- Move people to right teams if needed
- Update career ladders
- Monitor for confusion

---

## Golden Path Template Design

**When to Use:** Creating a "golden path" pipeline template or infrastructure template for common use cases.

**Related Resources:**
- [Platform Engineering for Azure](../practices/platform-engineering-azure.md)
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)

**The Prompt:**
```
I want to create a golden path template for [use case, e.g., ".NET API" or "React SPA" or "Python Azure Function"].

Context:
- Common use case: [describe what teams repeatedly build]
- Current pain points: [inconsistency, security gaps, manual steps, etc.]
- Technology stack: [.NET 8, React, Python, etc.]
- Required capabilities: [CI/CD, testing, security scanning, deployment, etc.]
- Security requirements: [Defender for DevOps, policy compliance, etc.]
- Target audience: [skill level of teams who'll use this]

Design a golden path that:
1. Makes the right thing the easy thing (security, monitoring, testing built-in)
2. Balances opinionated defaults with necessary flexibility
3. Provides escape hatches for edge cases
4. Is well-documented and easy to adopt
5. Follows Azure best practices

Reference the platform engineering guides for golden path patterns.
```

**Expected Output:**
- Template design (pipeline YAML or Bicep structure)
- Opinionated defaults with clear rationale
- Parameterization strategy
- Security and quality built-in
- Documentation outline
- Getting started guide

**Follow-Up Actions:**
- Build template
- Create comprehensive docs
- Pilot with one team
- Gather feedback
- Iterate and improve
- Evangelize to other teams

---

## Cognitive Load Assessment

**When to Use:** You suspect a team is overwhelmed or spread too thin.

**Related Resources:**
- [Team Topologies](../practices/team-topologies.md) - Cognitive Load section
- [Team Topologies Anti-Patterns](../practices/team-topologies-anti-patterns.md) - Ignoring Cognitive Load section

**The Prompt:**
```
I'm concerned that [team name] has too much cognitive load.

Team details:
- Team size: [number]
- Services owned: [list all]
- Technologies used: [languages, frameworks, tools]
- Recent incidents: [frequency and patterns]
- Innovation work: [when was the last improvement project?]
- Team feedback: [complaints about being overwhelmed, burnout signs, etc.]

Help me:
1. Assess cognitive load (intrinsic, extraneous, germane)
2. Identify if team owns too many services
3. Determine if technology diversity is too high
4. Recommend actions (split team, reduce scope, platform support, etc.)
5. Create plan to reduce load

Reference the Team Topologies guide for cognitive load framework and the anti-patterns guide for solutions.
```

**Expected Output:**
- Cognitive load assessment (intrinsic, extraneous, germane)
- Identification of load sources
- Recommendations (sunset services, split team, platform capabilities)
- Action plan to reduce load
- Success metrics

**Follow-Up Actions:**
- Discuss with team
- Sunset or hand off low-value services
- Request platform support for extraneous load
- Consider team split if needed
- Regular cognitive load check-ins

---

## Platform Roadmap Planning

**When to Use:** Planning the platform team's roadmap based on product team needs.

**Related Resources:**
- [Platform Engineering & DevEx](../practices/platform-engineering-devex.md)
- [Planning & Prioritization](../practices/planning-prioritization.md)

**The Prompt:**
```
I need to create a platform roadmap for [time period, e.g., "next quarter" or "next 6 months"].

Input:
- Product team feedback: [requests, pain points, complaints]
- Current platform services: [what exists]
- Gaps: [what teams build repeatedly]
- DORA metrics: [current state and targets]
- Developer satisfaction: [NPS or survey results]
- Platform team capacity: [number of engineers]

Help me:
1. Categorize requests (self-service capabilities, golden paths, enablement, etc.)
2. Prioritize using impact vs effort
3. Balance quick wins with strategic capabilities
4. Create roadmap with milestones
5. Set success metrics for each capability

Reference the platform engineering & DevEx guide for good platform capabilities, and planning/prioritization for frameworks.
```

**Expected Output:**
- Categorized and prioritized backlog
- Roadmap with timeline
- Quick wins to build momentum
- Strategic capabilities
- Success metrics for each item
- Capacity plan

**Follow-Up Actions:**
- Share roadmap with product teams
- Gather feedback
- Execute on quick wins
- Build strategic capabilities
- Measure impact and iterate

---

## Team Capacity Planning

**When to Use:** Stakeholders ask when their work will be done, demand is exceeding capacity, or you need to structure how work is scheduled across multiple squads.

**Related Resources:**
- [Capacity Planning & Scheduling](../practices/capacity-planning-scheduling.md)
- [Planning & Prioritization](../practices/planning-prioritization.md)
- [Stakeholder Management](../leadership/stakeholder-management.md)

**The Prompt:**
```
My Platform/DevOps team serves multiple squads and I'm struggling to manage demand fairly and give stakeholders clear answers about when work will get done.

Current situation:
- Team size: [number of engineers]
- Squads we serve: [list squads and their typical request volume]
- Current intake process: [ad hoc / some structure / formal]
- Biggest pain points: [everything feels urgent / stakeholders unhappy / team overwhelmed / no visibility into queue]
- Current capacity split: [do you know where time goes?]
- Unplanned work level: [how often does unplanned work disrupt plans?]

Help me design a capacity planning system:
1. Calculate true available capacity (accounting for operational, support, overhead)
2. Design a work intake and classification model (Critical / Urgent / Standard)
3. Define SLA commitments for each request class
4. Create an allocation model across squads and work types
5. Build a queue management approach with honest wait time communication
6. Design a monthly stakeholder update to maintain trust
7. Identify metrics to track capacity health

Reference the capacity planning & scheduling guide for frameworks and templates.
```

**Expected Output:**
- True capacity calculation with realistic deductions
- Work classification system with SLA tiers
- Capacity allocation model (% per work type)
- Queue management approach with wait time formula
- Stakeholder communication templates
- Capacity health metrics dashboard

**Follow-Up Actions:**
- Set up intake backlog in Azure DevOps/Jira
- Publish SLAs on team wiki
- Run first weekly triage
- Send first monthly capacity snapshot
- Track metrics for 2-3 sprints to establish baseline

---

## Capacity Overload Escalation

**When to Use:** Demand is consistently exceeding your team's capacity and you need to escalate to leadership for more headcount or priority trade-offs.

**Related Resources:**
- [Capacity Planning & Scheduling](../practices/capacity-planning-scheduling.md) - Demand forecasting and escalation sections
- [Stakeholder Management](../leadership/stakeholder-management.md) - Managing up

**The Prompt:**
```
My Platform/DevOps team is consistently overloaded and I need to escalate to leadership.

The data:
- Team capacity (planned work): [X hours/sprint]
- Average demand: [X hours/sprint]
- Deficit per sprint: [X hours]
- Duration of overload: [X months]
- Queue: [X items, oldest is X weeks]
- SLA compliance: [X% vs target X%]
- Impact: [describe blocked squads, delayed releases, or team burnout signs]

I need to:
1. Build a clear business case showing the supply/demand gap
2. Present options (hire / reduce scope / self-service investment / prioritise only X squads)
3. Communicate impact of inaction
4. Get a leadership decision

Help me prepare for this escalation conversation using the capacity planning guide frameworks.
```

**Expected Output:**
- Business case with data-backed narrative
- Options presented with trade-offs (not just "hire someone")
- Impact of inaction framed in business terms (delayed releases, risk, burnout)
- Recommendation
- Conversation structure for leadership meeting

**Follow-Up Actions:**
- Schedule meeting with your manager and relevant stakeholders
- Bring capacity data and queue visualisation
- Get a decision, not just acknowledgement
- Follow up in writing

---

## Related Prompt Banks

- [Leadership Prompts](leadership-prompts.md) - Feedback, performance, coaching
- [Team Prompts](team-prompts.md) - Team health and dynamics
- [Technical Prompts](technical-prompts.md) - Technical decisions and architecture
- [Strategic Prompts](strategic-prompts.md) - Planning and prioritization

# Avoiding Team Topologies Anti-Patterns

## Overview

Team Topologies provides a powerful framework, but implementation can easily drift into anti-patterns that undermine the benefits. This guide provides **specific guardrails, warning signs, and corrective actions** to help you avoid common pitfalls.

**Key Principle:** Anti-patterns typically emerge from good intentions but incorrect mental models. Most can be prevented through clear principles, regular health checks, and willingness to course-correct.

---

## Anti-Pattern #1: "DevOps Team" as a Silo

### The Problem

Creating a separate "DevOps team" that handles deployments, infrastructure, or operations for everyone else.

**Why It Happens:**
- Misunderstanding of DevOps (it's a culture, not a role)
- Fear that product teams "can't be trusted" with production
- Trying to centralize expertise
- Legacy ops team rebranded as "DevOps"

**Why It's Harmful:**
- Creates bottleneck (handoffs, tickets, waiting)
- Product teams don't learn operational skills
- "Throw it over the wall" mentality persists
- DevOps team becomes overwhelmed
- Slows deployment frequency dramatically

### How to Avoid It

#### 1. Clarify the Mental Model

**Wrong Model:**
```
Product Team → Builds code → Hands to DevOps Team → DevOps Team deploys/operates
```

**Right Model:**
```
Stream-Aligned Team → Builds, deploys, operates their own services
                    ↓ (consumes services from)
Platform Team → Provides self-service tools/infrastructure
                    ↓ (gets coaching from)
Enabling Team → Teaches DevOps practices
```

#### 2. Embed DevOps Skills in Product Teams

**Actions:**
- Hire or upskill product team members with infrastructure/automation skills
- Include "deploy to production" in team's definition of done
- Product teams own their on-call rotation
- No separate deployment approval from another team

**Example Team Composition:**
- 3 backend developers (one with strong Azure/infrastructure skills)
- 2 frontend developers
- 1 QA engineer (automation focus)
- 1 product manager
= **Cross-functional team that can deploy end-to-end**

#### 3. Transform "DevOps Team" into Platform Team

If you already have a DevOps team, **rebrand and refocus** as a platform team:

**Before (Anti-Pattern):**
- Team receives deployment tickets
- Team manually deploys for product teams
- Team owns all infrastructure
- Ticket-based model

**After (Platform Team):**
- Team builds self-service deployment pipelines
- Product teams deploy themselves using platform tools
- Team provides Bicep modules, pipeline templates
- Self-service model with support channel

**Transition Steps:**
1. **Week 1-2:** Announce shift to platform team model, explain why
2. **Week 3-4:** Identify first self-service capability to build (e.g., pipeline template)
3. **Month 2:** Pilot with one product team using self-service
4. **Month 3:** Roll out to all teams, deprecate ticket-based deployments
5. **Ongoing:** Platform team roadmap driven by product team needs

#### 4. Establish Clear Principles

**Principles to Communicate:**
- "You build it, you run it" - teams own their services end-to-end
- Platform team provides tools, not deployment services
- Self-service is the goal, tickets are temporary
- Product teams are trusted with production access

#### 5. Set Up Guardrails, Not Gates

**Anti-Pattern (Gates):**
- Require manual approval from DevOps team for every deployment
- Tickets for infrastructure changes
- No production access for product teams

**Better Approach (Guardrails):**
- Automated security scanning in pipeline (fails build if issues found)
- Policy as Code (Azure Policy prevents misconfigurations)
- Automated rollback on failed health checks
- Observability to detect issues quickly
- Product teams have production access with audit logging

**Example Azure Implementation:**
```yaml
# Pipeline with automated guardrails
stages:
  - stage: Build
    jobs:
      - job: BuildAndTest
        steps:
          - task: DotNetCoreCLI@2
          - task: WhiteSourceBolt  # Security scanning

  - stage: Deploy_Dev
    jobs:
      - deployment: DeployDev
        environment: dev

  - stage: SecurityValidation
    jobs:
      - job: DefenderScan
        steps:
          - task: MicrosoftSecurityDevOps@1  # Defender for DevOps
          - script: |
              # Fail if critical vulnerabilities found
              if [ $CRITICAL_COUNT -gt 0 ]; then exit 1; fi

  - stage: Deploy_Prod
    jobs:
      - deployment: DeployProd
        environment: production  # Can require business approval, not DevOps team approval
        strategy:
          runOnce:
            deploy:
              steps:
                - task: AzureWebApp@1
                - task: HealthCheck  # Auto-rollback if fails
```

### Warning Signs You're in This Anti-Pattern

- [ ] Product teams submit tickets to deploy their code
- [ ] "DevOps team" is a bottleneck mentioned in retrospectives
- [ ] Deployment frequency is low (less than weekly)
- [ ] Product teams don't have production access
- [ ] DevOps team backlog is always growing
- [ ] Product teams say "we're waiting on DevOps"
- [ ] DevOps team has no time for improvement work (only reactive)

### How to Course-Correct

**If you're already in this pattern:**

1. **Measure the pain** (make it visible):
   - Track deployment lead time (request to production)
   - Count tickets waiting in DevOps queue
   - Survey product teams on biggest bottlenecks

2. **Pick one product team for pilot**:
   - Give them self-service deployment capability
   - Platform team builds pipeline template for them
   - Measure before/after (deployments per week, lead time)

3. **Show the results**:
   - "Pilot team now deploys 10x/week instead of 2x/week"
   - "Lead time went from 3 days to 4 hours"
   - Use data to convince stakeholders

4. **Scale gradually**:
   - Roll out to next team
   - Build platform capabilities as you go
   - Deprecate ticket-based model

5. **Celebrate the transition**:
   - Publicly recognize platform team's new role
   - Share success stories
   - Update job descriptions and career paths

---

## Anti-Pattern #2: Matrix Management

### The Problem

People reporting to multiple managers or having unclear accountability due to dotted-line reporting structures.

**Why It Happens:**
- Trying to balance functional expertise with project needs
- Spotify model misinterpretation (chapter leads as managers)
- Fear of losing functional expertise
- Traditional hierarchical thinking

**Why It's Harmful:**
- Unclear accountability ("who's actually my boss?")
- Conflicting priorities between managers
- Performance review confusion
- Slower decision-making (need multiple approvals)
- People feel torn between competing demands

### How to Avoid It

#### 1. Single Clear Reporting Line

**Principle:** Everyone has exactly **one manager** who is responsible for:
- Performance reviews
- Career development
- Compensation decisions
- Priority setting
- Hiring/firing decisions

**Structure:**
```
Product Team Structure:
- Engineering Manager (EM) → manages entire team
  ├── Backend Developer 1
  ├── Backend Developer 2
  ├── Frontend Developer 1
  ├── Frontend Developer 2
  └── DevOps Engineer

NOT:
- Engineering Manager → manages some aspects
- Chapter Lead → manages other aspects (CONFLICT)
```

#### 2. Use Chapters for Community, Not Management

**Chapters Done Right (Not Matrix Management):**
- **Purpose:** Community of practice for skill development
- **Chapter Lead:** Senior engineer who facilitates, does NOT manage
- **Activities:** Knowledge sharing, standards, training, hiring input
- **No Authority Over:** Performance reviews, priorities, compensation

**Example:**
- **Backend Chapter:** All backend engineers across teams meet monthly
  - Share patterns and anti-patterns
  - Discuss technology choices
  - Review architectural decisions
  - Chapter lead is a Staff/Principal Engineer
  - **But:** Everyone still reports to their team's Engineering Manager

#### 3. Clear Decision Rights

Use a RACI or DACI framework to clarify who decides what:

**Example Decision Rights Matrix:**

| Decision | Team EM | Chapter Lead | Product Manager | Platform Team |
|----------|---------|--------------|-----------------|---------------|
| Team priorities | **A** | C | **R** | I |
| Technology choice | **A** | **R** | C | C |
| Performance review | **AR** | C | I | - |
| Architecture standards | C | **AR** | I | C |
| Platform tools | C | C | I | **AR** |

**Legend:** R = Responsible, A = Accountable, C = Consulted, I = Informed

#### 4. Temporary Project Assignments ≠ Reporting Line

**When someone works on cross-team initiatives:**
- They still report to their home team manager
- Project lead has authority over project deliverables
- Home manager handles performance, priorities, career

**Example:**
- Frontend developer joins a 3-month initiative to build design system
- Reports to: Frontend Team Engineering Manager (unchanged)
- Works with: Design System Project Lead (temporary)
- After 3 months: Returns to frontend team or transitions to design system team (single reporting line)

### Warning Signs You're in This Anti-Pattern

- [ ] Engineers don't know who to ask for time off
- [ ] "Who's my manager?" is a genuine question
- [ ] Performance reviews involve multiple people giving ratings
- [ ] Conflicting priorities from different "managers"
- [ ] Chapter leads behave like functional managers
- [ ] Org chart has dotted lines everywhere
- [ ] People spending significant time reconciling competing demands

### How to Course-Correct

1. **Audit reporting structure**:
   - Draw current org chart
   - Mark every dotted line
   - Ask: "Who actually does performance reviews?"

2. **Clarify one manager per person**:
   - Announce clear reporting lines
   - Update HRIS system
   - Communicate to entire org

3. **Redefine chapter/guild roles**:
   - Chapter leads are facilitators, not managers
   - Purely for community and skill development
   - No authority over performance or priorities

4. **Document decision rights**:
   - Create RACI for common decisions
   - Publish and socialize
   - Use in onboarding

---

## Anti-Pattern #3: Projects Over Products

### The Problem

Forming temporary teams for projects, then disbanding them when the project "ends."

**Why It Happens:**
- Traditional project management thinking
- "Efficient resource utilization" mindset
- Budget allocated per project, not product
- Consultant/agency background

**Why It's Harmful:**
- No long-term ownership (nobody maintains the code)
- Knowledge lost when team disbanded
- No operational responsibility
- Incentive to cut corners (you won't be around to deal with it)
- Constant team forming/storming overhead
- People optimized for project completion, not product success

### How to Avoid It

#### 1. Organize Around Products/Value Streams, Not Projects

**Anti-Pattern:**
```
Project: Customer Portal Redesign (6 months)
- Form team of 8 people
- Build new portal
- Launch
- Team disbanded
- Portal becomes "legacy" immediately (nobody owns it)
```

**Better Approach:**
```
Product Team: Customer Portal Team (ongoing)
- Long-lived team of 6-8 people
- Owns the portal forever
- Roadmap includes: redesign, then ongoing features, maintenance, operations
- Team evolves the product continuously
```

#### 2. Stable Teams with Evolving Missions

**Principle:** Keep team together, change their mission as priorities shift.

**Example:**
- **Year 1:** Customer Portal Team builds initial portal
- **Year 2:** Team adds authentication improvements, performance optimization
- **Year 3:** Team rebuilds checkout flow
- **Throughout:** Team operates and maintains everything they've built

**Benefits:**
- Team builds deep context
- Continuous improvement mindset
- Operational excellence (you live with what you build)
- Lower onboarding overhead

#### 3. Fund Teams, Not Projects

**Budget Model Shift:**

**Old Model (Projects):**
- Budget request: "Customer Portal Redesign - $500K, 6 months"
- Approval based on project ROI
- Team formed for project
- After project: team disbanded, reallocated

**New Model (Products):**
- Budget request: "Customer Portal Team - 7 people, ongoing"
- Team has roadmap with multiple initiatives
- Annual planning adjusts team size based on strategic priority
- Team continuously delivers value

**How to Present to Finance:**
- Show total cost of ownership (development + operations)
- Long-lived teams have lower overhead (no forming/storming)
- Better quality from ownership
- Faster delivery from stability

#### 4. Outcome-Focused Roadmaps, Not Fixed-Scope Projects

**Instead of:**
- "Project: Implement payment feature - 3 months, fixed scope"

**Use:**
- "Outcome: Increase successful checkout rate from 65% to 80%"
- Team has quarterly objectives
- They decide how to achieve outcomes
- Scope adjusts based on learning

#### 5. Handle Team Size Changes Gracefully

**When priorities shift and team needs to shrink:**
- **Don't disband:** Keep core team intact (maybe 4-5 people)
- Transition engineers to other teams (permanent moves)
- Team continues with smaller roadmap

**When team needs to grow:**
- Add people permanently
- Invest in onboarding
- Expect 3-month ramp-up time

### Warning Signs You're in This Anti-Pattern

- [ ] Teams are formed for initiatives then disbanded
- [ ] "Who owns this service?" has no clear answer
- [ ] Services have been in "maintenance mode" for years
- [ ] Budget process focuses on project approvals
- [ ] People frequently switch teams (every 6-12 months)
- [ ] Technical debt grows because "nobody owns it"
- [ ] Production issues have no clear owner

### How to Course-Correct

1. **Map current products/services**:
   - List all applications/services in production
   - Note who currently "owns" each (if anyone)

2. **Define long-lived product teams**:
   - Align teams to value streams
   - Assign ownership of existing services
   - Make it permanent (not project-based)

3. **Shift budget conversations**:
   - Present team capacity instead of project estimates
   - Roadmap shows outcomes, not fixed projects
   - Annual planning adjusts team sizes

4. **Communicate ownership**:
   - Public registry of team ownership
   - Every service has a team name
   - On-call rotation = ownership

---

## Anti-Pattern #4: Too Many Dependencies

### The Problem

Teams cannot deliver features without coordinating with 3+ other teams. Every initiative requires cross-team synchronization.

**Why It Happens:**
- Team boundaries don't align with value streams
- Shared databases or monolithic services
- Organizational structure mirrors old architecture
- "Efficiency" of shared services taken too far

**Why It's Harmful:**
- Slows everything down (waiting on other teams)
- Coordination overhead dominates actual work
- Features take months instead of weeks
- Meeting proliferation (sync meetings for everything)
- Teams lose autonomy and motivation

### How to Avoid It

#### 1. Design Team Boundaries for Minimal Dependencies

**Principle:** Teams should be able to deliver value end-to-end with minimal coordination.

**Good Boundary Examples:**
- **Customer Portal Team:** Owns entire customer-facing experience (frontend + backend APIs + database)
- **Payments Team:** Owns payment processing flow end-to-end
- Each team has their own databases, services, deployment pipeline

**Poor Boundary Examples:**
- **Frontend Team** + **Backend Team** + **Database Team** = Every feature requires all three teams
- Teams organized by technology layer instead of business capability

#### 2. Use APIs and Contracts, Not Shared Databases

**Anti-Pattern:**
```
Team A ──→ Shared Database ←── Team B
         (both read/write same tables)
```

**Result:** Every schema change requires coordination, teams can't move independently.

**Better Approach:**
```
Team A ──→ Team A's Database
           ↓ (publishes events or API)
Team B ──→ Listens to events / Calls API
       ──→ Team B's Database
```

**Implementation in Azure:**
```csharp
// Team A exposes API, owns database
public class PaymentService
{
    public async Task<PaymentResult> ProcessPayment(PaymentRequest request)
    {
        // Team A owns this database
        await _paymentDb.SaveAsync(payment);

        // Publish event for other teams
        await _serviceBus.PublishAsync(new PaymentProcessedEvent
        {
            PaymentId = payment.Id,
            Amount = payment.Amount,
            Status = payment.Status
        });

        return result;
    }
}

// Team B consumes events, has own database
public class OrderService
{
    public async Task HandlePaymentProcessed(PaymentProcessedEvent @event)
    {
        // Team B owns this database
        var order = await _orderDb.GetAsync(@event.OrderId);
        order.PaymentStatus = @event.Status;
        await _orderDb.SaveAsync(order);
    }
}
```

**Benefits:**
- Teams deploy independently
- Schema changes don't require coordination
- Clear contracts via APIs/events
- Eventual consistency is acceptable for most use cases

#### 3. Minimize Synchronous Dependencies

**Dependency Hierarchy (Best to Worst):**

1. **No dependency** (best) - Team is fully self-sufficient
2. **Asynchronous dependency** - Team publishes events, others consume when ready
3. **Well-defined API** - Team calls another team's API, but it's stable and documented
4. **Collaboration required** - Teams must coordinate on changes (temporary, for discovery)
5. **Synchronous handoff** - Team waits for another team to do something (worst)

**Goal:** Most dependencies should be #1-3.

#### 4. Measure and Track Dependencies

**Dependency Mapping Exercise:**

Create a matrix showing which teams depend on which:

|  | Portal Team | Payments Team | Mobile Team | Platform Team |
|--|-------------|---------------|-------------|---------------|
| **Portal Team** | - | API calls (stable) | - | Consumes platform |
| **Payments Team** | Events | - | API calls | Consumes platform |
| **Mobile Team** | API calls | API calls | - | Consumes platform |
| **Platform Team** | - | - | - | - |

**Red Flags:**
- Many cells marked "Requires coordination"
- Circular dependencies
- Shared database access

**Quarterly Review:**
- Count blocking dependencies per team
- Track time spent in cross-team coordination
- Identify most problematic dependencies
- Refactor to reduce

#### 5. Platform Team as Acceptable Dependency

**Note:** Dependencies on platform team are acceptable because:
- Platform provides X-as-a-Service (self-service, no coordination needed)
- Stable APIs/interfaces
- Platform team treats product teams as customers

**Example:**
- All teams depend on platform for Bicep modules → **Good** (self-service)
- All teams must ask platform team for deployments → **Bad** (bottleneck)

### Warning Signs You're in This Anti-Pattern

- [ ] Features require 3+ teams to coordinate
- [ ] Teams have "dependency" swimlane in their board
- [ ] Many shared databases with multiple teams reading/writing
- [ ] Scrum of scrums or similar coordination meetings
- [ ] "Blocked waiting on Team X" appears frequently
- [ ] Teams can't deploy independently
- [ ] Integration issues are common

### How to Course-Correct

1. **Map current dependencies**:
   - Create dependency matrix
   - Identify most problematic dependencies
   - Categorize (can we eliminate? Reduce? Accept?)

2. **Refactor team boundaries** (if needed):
   - Realign teams to value streams
   - Consider moving people to reduce dependencies
   - Example: Move backend engineer from "API team" to "Customer Portal team"

3. **Break apart shared databases**:
   - Start with one shared database
   - Create APIs for access
   - Gradually move to separate databases with event-driven integration

4. **Establish API contracts**:
   - Document and version APIs
   - Semantic versioning
   - Backward compatibility commitments

5. **Timebox collaboration**:
   - When collaboration needed, set explicit end date
   - Example: "Teams will collaborate for 4 weeks to define payment API, then move to X-as-a-Service"

---

## Anti-Pattern #5: Platform as a Ticket System

### The Problem

Platform team operates as a ticketing/approval system rather than providing self-service capabilities.

**Why It Happens:**
- Control mindset ("we need to approve everything")
- Compliance misinterpretation ("security requires manual review")
- Legacy ITIL/ITSM processes
- Platform team overwhelmed, falls back to tickets

**Why It's Harmful:**
- Platform team becomes bottleneck
- Defeats the purpose of platform engineering
- Developer experience is terrible
- Slow delivery (waiting for tickets)
- Platform team burns out from ticket volume

### How to Avoid It

#### 1. Self-Service as Primary Interface

**Principle:** 80%+ of common requests should be self-service, no ticket required.

**Self-Service Examples:**

**Azure Dev Box Provisioning:**
```powershell
# Developer runs this themselves, no ticket
az devcenter dev dev-box create \
  --name "mydevbox" \
  --dev-center-name "platform-devcenter" \
  --pool-name "dotnet-pool"

# Provisioned in minutes, automatically has security baseline
```

**Infrastructure Provisioning via Bicep Module:**
```bicep
// Developer uses platform module, self-service deployment
module webApp 'br:platformregistry.azurecr.io/bicep/web-app:v1.2.0' = {
  name: 'myWebApp'
  params: {
    appName: 'my-api'
    environment: 'dev'
    // Security, monitoring, naming conventions built-in
  }
}

// Developer runs:
// az deployment group create --template-file main.bicep
// No approval needed, policy prevents misconfigurations
```

**Pipeline Template (Golden Path):**
```yaml
# Developer extends template, self-service
extends:
  template: dotnet-api-template.yml@platform-templates
  parameters:
    serviceName: 'my-new-api'
    # Everything else is preconfigured

# Commit and push → pipeline runs automatically
# No approval needed for dev, automated checks for production
```

#### 2. Guardrails via Automation, Not Approvals

**Replace Manual Approvals With:**

**Azure Policy (Preventive Controls):**
```bicep
// Platform team sets policies
resource policy 'Microsoft.Authorization/policyDefinitions@2021-06-01' = {
  properties: {
    policyRule: {
      if: {
        allOf: [
          {
            field: 'type'
            equals: 'Microsoft.Storage/storageAccounts'
          }
          {
            field: 'Microsoft.Storage/storageAccounts/allowBlobPublicAccess'
            equals: 'true'
          }
        ]
      }
      then: {
        effect: 'deny'  // Prevents misconfiguration, no approval needed
      }
    }
  }
}
```

**Automated Security Scanning:**
```yaml
# In pipeline template, automatic checks
- task: MicrosoftSecurityDevOps@1
  displayName: 'Security scan (automatic)'

- script: |
    if [ $CRITICAL_VULNS -gt 0 ]; then
      echo "Critical vulnerabilities found, deployment blocked"
      exit 1
    fi
```

**Cost Guardrails:**
```powershell
# Automated cost check in pipeline
$estimatedCost = Get-AzureResourceCost -TemplateFile main.bicep
if ($estimatedCost -gt $threshold) {
    Write-Error "Estimated cost exceeds threshold, manager approval required"
    # Only expensive deployments need approval, not all deployments
}
```

#### 3. Ticket System for Exceptions Only

**Use Tickets For:**
- ✅ Requests outside of self-service capabilities (edge cases)
- ✅ New capability requests for platform roadmap
- ✅ Support when self-service fails
- ✅ Security exceptions (e.g., need to disable a policy)

**Do NOT Use Tickets For:**
- ❌ Routine deployments
- ❌ Creating dev environments
- ❌ Using existing platform services
- ❌ Standard infrastructure provisioning

#### 4. Measure Self-Service Success

**Metrics to Track:**
| Metric | Target | Why It Matters |
|--------|--------|----------------|
| Self-service success rate | >90% | How often devs succeed without support |
| Ticket volume trend | Decreasing | Better docs/tools mean fewer tickets |
| Time to provision (self-service) | <1 hour | Fast feedback loop |
| Time to provision (via ticket) | <4 hours | Even exceptions should be fast |
| Platform NPS score | >40 | Overall satisfaction |
| Adoption rate | >80% | Are teams using platform services |

#### 5. Documentation and Discoverability

**Self-Service Requires Great Docs:**

**Developer Portal (Example Structure):**
```
Platform Portal
├── Getting Started
│   ├── Your First Web App (5 min)
│   ├── Your First Database (5 min)
│   └── Your First Pipeline (10 min)
├── Bicep Modules
│   ├── Web Apps (examples, parameters)
│   ├── Databases (examples, parameters)
│   └── Storage (examples, parameters)
├── Pipeline Templates
│   ├── .NET API Template
│   ├── React SPA Template
│   └── Python Function Template
├── Azure Dev Box
│   ├── Create Your Dev Box (guide)
│   └── Available Configurations
├── How-To Guides
│   ├── Add a Database to Your App
│   ├── Enable Custom Domain
│   └── Set Up Monitoring
└── Support
    ├── Slack Channel: #platform-help
    ├── Office Hours: Tuesdays 2-3pm
    └── Submit Ticket (for exceptions)
```

**Every self-service capability needs:**
- Quick start guide (5-10 minutes to success)
- Code examples (copy-paste ready)
- Parameter reference
- Troubleshooting section
- When to ask for help

### Warning Signs You're in This Anti-Pattern

- [ ] Platform team backlog is mostly tickets
- [ ] "Waiting on platform approval" is common phrase
- [ ] Developers complain about platform team responsiveness
- [ ] Most requests take days (not minutes/hours)
- [ ] Platform team has no time for roadmap/improvements
- [ ] Deployment requires manual approval from platform team
- [ ] Ticket volume is increasing, not decreasing

### How to Course-Correct

1. **Audit current tickets**:
   - Categorize last 100 tickets
   - Identify most common requests
   - Ask: "Could this be self-service?"

2. **Build self-service for top 3 ticket types**:
   - Example: "Create dev environment" → Azure Dev Box self-service
   - Example: "Deploy new web app" → Bicep module + pipeline template
   - Example: "Add database" → Bicep module

3. **Set expectation shift**:
   - Announce: "These capabilities are now self-service"
   - Provide migration guide
   - Deprecate ticket-based approach for these

4. **Measure adoption**:
   - Track self-service usage vs tickets
   - Gather feedback
   - Iterate on docs and UX

5. **Celebrate ticket reduction**:
   - "Tickets down 60% because of self-service!"
   - Free up platform team for strategic work

---

## Anti-Pattern #6: Ignoring Cognitive Load

### The Problem

Teams are responsible for too many services, technologies, or domains. They're spread too thin.

**Why It Happens:**
- "Efficiency" mindset (one team can handle multiple things)
- Underestimating complexity
- Reluctance to hire more people
- Not recognizing cognitive load as a constraint

**Why It's Harmful:**
- Quality suffers (too much to keep in mind)
- Incidents increase (lack of deep knowledge)
- Burnout (constantly context switching)
- Slow delivery (everything takes longer)
- Innovation stops (no capacity for improvement)

### How to Avoid It

#### 1. Assess Cognitive Load Regularly

**Simple Assessment Framework:**

Ask teams to rate their cognitive load (1-10 scale):

**Intrinsic Load:** Domain complexity, business logic
**Extraneous Load:** Tooling complexity, process overhead, how to deploy/operate
**Germane Load:** Learning new patterns, innovation work

**Healthy Balance:**
- Intrinsic: 5-7 (appropriate for domain)
- Extraneous: 2-4 (minimal overhead thanks to platform)
- Germane: 2-3 (room for innovation)

**Danger Zone:**
- Intrinsic: 8-10 (domain too complex, consider splitting)
- Extraneous: 6-10 (too much tooling complexity, platform team should help)
- Germane: 0 (no innovation capacity, team is underwater)

#### 2. Limit Services Per Team

**Guideline:** Stream-aligned team should own **3-8 services** depending on complexity.

**Warning Signs of Too Many:**
- Team can't remember all services they own
- Incidents in services they "forgot about"
- No time for proactive improvement
- Long onboarding time for new team members

**Example Right-Sized Ownership:**

**Payments Team (6 people) owns:**
1. Payment API (high complexity, high criticality)
2. Payment Processing Functions (medium complexity)
3. Payment Admin Dashboard (low complexity)
= **3 services, appropriate cognitive load**

**Red Flag Example:**

**Internal Tools Team (5 people) owns:**
1. Admin Dashboard
2. Reporting Service
3. Data Export Tool
4. Notification Service
5. User Management System
6. Audit Log Service
7. Configuration Service
8. Analytics Platform
9. Internal API Gateway
10. Legacy Migration Tool
= **10 services, way too much cognitive load**

**Solution:** Split into two teams or sunset/consolidate services.

#### 3. Technology Diversity Management

**Limit Tech Stack Breadth:**

**Good (Focused):**
- Languages: C#, TypeScript
- Frontend: React
- Infrastructure: Bicep, PowerShell
- Data: SQL Server, Cosmos DB
- Messaging: Service Bus

**Problematic (Too Diverse):**
- Languages: C#, TypeScript, Python, Go, Java
- Frontend: React, Angular, Vue
- Infrastructure: Bicep, Terraform, ARM templates, PowerShell, Bash
- Data: SQL Server, PostgreSQL, MySQL, Cosmos DB, MongoDB, Redis
- Messaging: Service Bus, Event Grid, Event Hub, RabbitMQ, Kafka

**Cognitive Load Impact:**
- Every additional technology = context switching
- Harder to build expertise
- More tooling to learn
- Different debugging approaches

**Platform Team's Role:**
- Provide golden paths for preferred stack
- Make standard stack the easy path
- Allow exceptions with justification

#### 4. Reduce Extraneous Load with Platform Services

**This is Platform Team's Primary Job:**

**Common Sources of Extraneous Load:**
- Complex deployment processes → **Solution:** Pipeline templates
- Manual infrastructure provisioning → **Solution:** Bicep modules
- Security configuration → **Solution:** Built into modules
- Monitoring setup → **Solution:** Auto-configured in templates
- Cost tracking → **Solution:** Platform provides dashboards
- Compliance requirements → **Solution:** Policy as Code

**Before Platform Investment:**
Team spends 40% time on extraneous load (how to deploy, configure, secure)

**After Platform Investment:**
Team spends 10% time on extraneous load, 90% on product

#### 5. Regular Cognitive Load Reviews

**Quarterly Health Check:**

**Facilitated Discussion (1 hour):**
1. What are we responsible for? (list all services, technologies)
2. What feels overwhelming? (identify high load areas)
3. What could we simplify? (sunset services, reduce tech diversity)
4. What platform services would help us? (input to platform roadmap)

**Actions:**
- Identify services to sunset or consolidate
- Request platform team support for high extraneous load
- Consider team split if intrinsic load too high

### Warning Signs You're in This Anti-Pattern

- [ ] Team owns 10+ services
- [ ] Team uses 5+ programming languages/major frameworks
- [ ] Onboarding takes 3+ months
- [ ] Team has no time for proactive improvements
- [ ] Burnout signals (attrition, sick leave)
- [ ] Quality issues increasing
- [ ] Team says "we're spread too thin"
- [ ] Incidents in services the team "forgot about"

### How to Course-Correct

1. **Audit team responsibilities**:
   - List all services owned
   - List all technologies used
   - Estimate complexity for each

2. **Cognitive load assessment**:
   - Survey team members
   - Identify what feels overwhelming

3. **Sunset or consolidate**:
   - Identify services with low value, high maintenance
   - Sunset or hand off to another team
   - Consolidate overlapping services

4. **Reduce technology diversity**:
   - Migrate to preferred stack where feasible
   - Standardize on fewer tools

5. **Request platform support**:
   - What extraneous load could platform reduce?
   - Prioritize platform roadmap based on this

6. **Consider team split**:
   - If intrinsic load is genuinely too high
   - Split into two focused teams

---

## Anti-Pattern #7: Copying Structure Without Context

### The Problem

Adopting another company's team structure (Spotify, Netflix, etc.) without understanding why it worked for them or if it fits your context.

**Why It Happens:**
- "Best practices" cargo culting
- Impressive conference talks
- Consultant recommendations
- Lack of confidence in own design

**Why It's Harmful:**
- What worked for Spotify in 2012 doesn't fit your 2026 context
- Different scale, culture, technology, market
- Misses the principles behind the structure
- Creates confusion and dysfunction

### How to Avoid It

#### 1. Understand Principles, Not Prescriptions

**When Learning from Other Companies:**

**Ask:**
- **Why** did they structure teams this way?
- What **problem** were they solving?
- What was their **context** (size, culture, tech stack)?
- What **changed** since they published this?
- What **didn't work** (they rarely talk about this)?

**Don't Ask:**
- "Can we copy this exactly?"

#### 2. Context Matters Enormously

**Example Contexts:**

**Spotify (when model was created):**
- ~500 engineers
- Consumer music streaming product
- Greenfield development
- Strong engineering culture
- Swedish culture (high trust, flat hierarchies)

**Your Company (example):**
- 50 engineers
- B2B SaaS product
- 10-year-old codebase
- Growing engineering culture
- Regulatory compliance requirements

**Applying Spotify Model Directly = Poor Fit**

**Instead, Extract Principles:**
- ✅ Principle: Small, autonomous teams aligned to value
- ✅ Principle: Balance autonomy with alignment
- ✅ Principle: Reduce dependencies between teams
- ❌ Structure: Exact squad/tribe/chapter structure

#### 3. Design for Your Context

**Your Constraints and Context:**
- Company size (50 vs 500 vs 5000 engineers)
- Product type (B2B vs B2C, SaaS vs product)
- Regulatory requirements (healthcare, finance, etc.)
- Existing architecture (greenfield vs legacy)
- Cultural norms (startup vs enterprise)
- Geographic distribution (co-located vs remote)
- Technology stack (cloud-native vs hybrid)

**Example Decision Making:**

**Question:** Should we have enabling teams?

**Small Company (30 engineers):**
- Probably not full-time enabling team
- Senior engineers do enabling part-time
- External consultants for specialized topics

**Medium Company (150 engineers):**
- 2-3 person enabling team makes sense
- Focus on biggest capability gaps
- Rotate senior engineers through enabling role

**Large Company (500+ engineers):**
- Multiple enabling teams for different domains
- Dedicated career path for enablement
- Formal engagement model

#### 4. Start with First Principles

**Team Topologies First Principles:**
1. Minimize cognitive load
2. Optimize for fast flow of change
3. Clear team boundaries and responsibilities
4. Team interaction modes that reduce coordination overhead

**Design Process:**
1. Identify your value streams
2. Design stream-aligned teams around them
3. Identify what platform services would reduce cognitive load
4. Determine if you need enabling teams (based on size, capability gaps)
5. Check for unnecessary complicated-subsystem teams (most orgs don't need them)

#### 5. Experiment and Iterate

**Approach:**
- Design your team structure based on principles and context
- **Pilot** with one or two teams
- Measure outcomes (DORA metrics, team satisfaction)
- Iterate based on learnings
- Scale what works

**Don't:**
- Reorganize entire company overnight
- Assume the design is final
- Ignore feedback from teams

### Warning Signs You're in This Anti-Pattern

- [ ] Justification for structure is "Company X does it"
- [ ] Structure doesn't match your value streams
- [ ] Teams don't understand why they're structured this way
- [ ] Copying naming without function (squads that aren't autonomous)
- [ ] Resistance from teams about new structure
- [ ] No measurement of whether structure is working
- [ ] Leadership can't explain principles behind structure

### How to Course-Correct

1. **Articulate principles**:
   - Why did we adopt this structure?
   - What problems were we trying to solve?
   - Are those still the right problems?

2. **Assess fit with your context**:
   - What's different about our situation?
   - What's not working?
   - What should we keep vs change?

3. **Redesign based on your context**:
   - Map your value streams
   - Design for your scale and culture
   - Keep what works, change what doesn't

4. **Communicate the "why"**:
   - Explain principles to teams
   - Connect structure to outcomes
   - Get buy-in through understanding

---

## Health Check Framework

Use this quarterly to assess if you're drifting into anti-patterns:

### Overall Team Health Survey

**Rate 1-5 (5 = Excellent):**

**Autonomy & Ownership:**
- [ ] My team can deploy changes without dependencies on other teams
- [ ] We have clear ownership of our services and domain
- [ ] We can make technology choices appropriate for our needs

**Cognitive Load:**
- [ ] Our team has a manageable number of services/responsibilities
- [ ] Platform services reduce our operational burden
- [ ] We have time for proactive improvement work

**Flow of Work:**
- [ ] We can deliver value to customers frequently (weekly or better)
- [ ] Waiting on other teams is rare
- [ ] Our deployment process is self-service

**Platform Experience:**
- [ ] Platform services make our work easier
- [ ] Platform team responds to our needs
- [ ] Self-service works most of the time

**Clarity:**
- [ ] I know who my manager is and who I report to
- [ ] Decision-making authority is clear
- [ ] Our team's mission and boundaries are clear

**Scores:**
- **20-25:** Healthy, well-functioning team structure
- **15-19:** Some issues, review low-scoring areas
- **10-14:** Significant anti-patterns, action needed
- **<10:** Major dysfunction, urgent redesign required

### Red Flag Indicators

**Immediate attention needed if:**
- [ ] Any team scores cognitive load >8 out of 10
- [ ] Deployment frequency decreased quarter over quarter
- [ ] Team attrition >20% per year
- [ ] Platform team backlog growing, not shrinking
- [ ] Most common answer to "why is this slow?" is "waiting on another team"

---

## Summary: Principles to Prevent Anti-Patterns

### Core Principles

1. **You Build It, You Run It**
   - Stream-aligned teams own end-to-end
   - No handoffs to separate ops team

2. **Platform Teams Are Product Teams**
   - Focus on self-service
   - Treat developers as customers
   - X-as-a-Service, not ticket-based

3. **One Manager, Clear Accountability**
   - No matrix management
   - Chapters for community, not management

4. **Long-Lived Teams, Evolving Missions**
   - Fund teams, not projects
   - Stable teams build context and ownership

5. **Design for Minimal Dependencies**
   - Team boundaries align to value streams
   - APIs, not shared databases
   - Asynchronous over synchronous

6. **Cognitive Load is the Constraint**
   - Limit services per team
   - Platform reduces extraneous load
   - Regular cognitive load reviews

7. **Context Over Cargo Culting**
   - Understand principles, not prescriptions
   - Design for your context
   - Experiment and iterate

---

## Related Resources

- [Team Topologies](team-topologies.md) - Core framework and concepts
- [Platform Engineering & Developer Experience](platform-engineering-devex.md)
- [Platform Engineering for Azure](platform-engineering-azure.md)
- [DevOps Career Ladder](devops-career-ladder.md)
- [Delegation](../leadership/delegation.md)
- [Difficult Conversations](../leadership/difficult-conversations.md) - For course corrections

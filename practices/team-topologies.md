# Team Topologies: Organizing for Flow and Fast Delivery

## Overview

Team Topologies provides a framework for organizing teams and their interactions to optimize for fast flow of change. It's based on recognizing that **how we organize teams determines how software is architected** (Conway's Law) and that **cognitive load is the limiting factor** in team effectiveness.

**Key Insight:** Most organizations struggle not because of technical problems, but because their team structures create communication overhead, unclear ownership, and cognitive overload.

## Core Concepts

### Conway's Law
> "Organizations which design systems are constrained to produce designs which are copies of the communication structures of these organizations."

**Translation:** Your architecture will mirror your organizational structure, whether you intend it or not.

**Implications:**
- If teams are siloed, your architecture will be tightly coupled
- If teams communicate through tickets/handoffs, your systems will have integration bottlenecks
- **Design your team structure intentionally to get the architecture you want**

### Cognitive Load

Teams have a **finite capacity** for information and complexity. Exceeding this load leads to:
- Slower delivery
- More bugs and incidents
- Burnout
- Context switching overhead

**Three types of cognitive load:**
1. **Intrinsic**: Fundamental aspects of the problem space (the domain knowledge needed)
2. **Extraneous**: About HOW to do work (deployment processes, tooling complexity, approvals)
3. **Germane**: Special aspects needing extra attention (learning new patterns, creative problem-solving)

**Team Topologies Goal:** Minimize extraneous load so teams can focus on intrinsic and germane work.

## The Four Fundamental Team Types

### 1. Stream-Aligned Teams (Product Teams)

**Purpose:** Build and deliver a steady flow of value aligned to a business stream

**Characteristics:**
- Cross-functional (full-stack capability)
- Owns a slice of the business domain or customer journey
- End-to-end ownership from development to production
- Long-lived, stable team (not project-based)
- Minimal dependencies on other teams

**Responsibilities:**
- Feature development for their stream
- Running what they build (you build it, you run it)
- User research and discovery
- Continuous improvement of their services

**Examples in Azure Context:**
- Customer Portal Team (owns the entire customer-facing web experience)
- Payments Team (owns payment processing flow)
- Mobile App Team (owns iOS/Android apps)

**Success Metrics:**
- Deployment frequency
- Lead time for changes
- Mean time to recovery
- Customer satisfaction with their features

**Cognitive Load Management:**
- Platform teams provide self-service capabilities (Azure modules, pipelines)
- Enabling teams help with new patterns and technologies
- Focus on business domain, not infrastructure complexity

---

### 2. Platform Teams (Internal Product Teams)

**Purpose:** Provide internal services that reduce cognitive load for stream-aligned teams

**Critical Mindset Shift:** Platform teams are **NOT** a "centralized operations team" or a "gatekeeper." They are an **internal product team** with stream-aligned teams as their customers.

**Characteristics:**
- Treat platform as a product with roadmap and UX
- Self-service is the goal (not tickets and approvals)
- Composed of capabilities, not just tools
- Strong focus on developer experience (DevEx)
- Reliability and ease of use are primary KPIs

**Responsibilities:**
- Building and maintaining internal developer platform (IDP)
- Golden paths and paved roads (easy, secure defaults)
- Self-service APIs and tooling
- Documentation and getting started guides
- Support and evangelism (but NOT gatekeeping)

**Examples in Azure Context:**
- **Platform Engineering Team:**
  - Bicep module library (web apps, databases, storage with security built-in)
  - Azure Pipeline templates (CI/CD golden paths)
  - PowerShell automation modules
  - Landing zone provisioning
  - Subscription vending machine
  - Cost reporting dashboards
  - Security baseline configurations (Defender for Cloud)
  - Development environment templates (Azure Dev Box)

**What Platform Teams Should NOT Do:**
- ❌ Require tickets for every deployment
- ❌ Be a bottleneck for change
- ❌ Mandate specific tools without providing value
- ❌ Build things nobody wants to use
- ❌ Ignore developer feedback

**What They SHOULD Do:**
- ✅ Make the right thing the easy thing
- ✅ Gather feedback and iterate on services
- ✅ Measure adoption and satisfaction
- ✅ Provide escape hatches for edge cases
- ✅ Document everything clearly

**Success Metrics:**
- Platform adoption rate (% of teams using platform services)
- Developer satisfaction (NPS scores)
- Time to provision new service (hours, not weeks)
- Reduction in incidents related to misconfigurations
- Support ticket volume (downward trend = better self-service)

---

### 3. Enabling Teams (Specialist Coaches)

**Purpose:** Help stream-aligned teams overcome capability gaps and adopt new technologies or practices

**Characteristics:**
- Small, specialist teams with deep expertise
- Work is **temporary and coaching-focused** (not doing work for other teams)
- Proactively identify gaps and emerging needs
- Write guides, run workshops, pair with teams
- Measure success by teams becoming self-sufficient

**Responsibilities:**
- Research and evaluation of new technologies
- Training and workshops
- Pairing with teams to transfer knowledge
- Creating guides and documentation
- Identifying patterns and anti-patterns

**Examples in Azure Context:**
- **Cloud Architecture Enablement:**
  - Help teams adopt Azure best practices
  - Review architecture designs
  - Terraform for multi-cloud scenarios
  - Azure governance patterns
- **Security & Compliance Enablement:**
  - Help teams meet security requirements
  - Threat modeling workshops
  - OWASP training
  - Defender for Cloud remediation guidance
- **Observability Enablement:**
  - Application Insights best practices
  - Distributed tracing patterns
  - Dashboard and alert design
- **DevOps Practices Enablement:**
  - Continuous deployment patterns
  - Testing strategies
  - Feature flag usage

**Interaction Model:**
- Enabling team **embeds** with stream-aligned team for 2-8 weeks
- They coach and pair, not take over the work
- Knowledge transfer is explicit (documentation, recordings)
- Engagement ends when team is self-sufficient
- Follow-up check-ins to ensure adoption

**Success Metrics:**
- Number of teams enabled (successfully transferred knowledge)
- Time to proficiency (how quickly teams become independent)
- Adoption rate of recommended practices
- Reduction in repeat questions/support tickets
- Team satisfaction with enablement experience

**Common Mistake:** Enabling teams becoming permanent dependencies. They should work themselves out of a job with each team.

---

### 4. Complicated-Subsystem Teams (Specialists)

**Purpose:** Reduce cognitive load for stream-aligned teams by owning complex subsystems requiring specialist knowledge

**Characteristics:**
- Small team with deep, specialized expertise
- Own a component that's too complex for stream-aligned teams to own
- Provide a well-defined interface/API
- Not every organization needs these teams

**Examples (General):**
- Video encoding/transcoding engine
- Real-time trading algorithm
- Mathematical modeling engine
- Face recognition API
- Machine learning model training platform

**Examples in Azure Context:**
- **Rarely needed in typical Azure organizations, but could include:**
  - AI/ML model training platform team
  - Real-time analytics engine (complex event processing)
  - Custom security encryption/HSM integration
  - Complex algorithm implementations (fraud detection, recommendation engines)

**When NOT to Create These:**
- ❌ When it's just unfamiliar technology (use enabling team instead)
- ❌ When it could be bought/outsourced (managed service)
- ❌ As an excuse to silo knowledge
- ❌ When it's organizational complexity, not technical complexity

**Success Metrics:**
- API/interface stability and ease of use
- Response time to stream-aligned team needs
- Reduction in complexity exposed to consumers
- Reliability of the subsystem

---

## The Three Interaction Modes

How teams interact is as important as team structure itself.

### 1. Collaboration Mode

**When:** Two or more teams work together for a defined period to discover interfaces or solve novel problems

**Characteristics:**
- High communication overhead (but temporary)
- Used for innovation and rapid discovery
- Teams have overlapping work
- Strong mutual respect required

**Example:**
- Stream-aligned team and platform team collaborate to design a new deployment pattern
- Two stream-aligned teams collaborate to integrate complex features
- Enabling team and stream-aligned team pair on security implementation

**Duration:** Weeks to a few months

**Exit Strategy:** Once interfaces are defined, switch to X-as-a-Service

**Warning:** Long-term collaboration creates dependencies and slows flow. It should be temporary.

---

### 2. X-as-a-Service Mode

**When:** One team provides something "as a service" to other teams with minimal collaboration

**Characteristics:**
- Clear API or interface (literal API, Bicep modules, pipeline templates, etc.)
- Self-service consumption
- Documentation-driven
- Low communication overhead
- Provider team treats it as a product

**Example:**
- Platform team provides Bicep modules consumed by stream-aligned teams
- Stream-aligned team exposes REST API consumed by other stream-aligned teams
- Enabling team provides training materials and docs consumed on-demand

**This should be the DEFAULT mode** for most platform-to-stream interactions.

**Success Factors:**
- Excellent documentation
- Clear versioning and change management
- Self-service portals/interfaces
- Responsive support for exceptions

---

### 3. Facilitating Mode

**When:** Enabling team helps stream-aligned team learn or adopt new capabilities

**Characteristics:**
- Coaching and mentoring focus
- Temporary engagement
- Knowledge transfer is explicit goal
- Hands-on pairing and collaboration

**Example:**
- Enabling team helps stream-aligned team adopt Terraform
- Security enabling team helps team implement threat modeling
- Platform team helps early adopters learn new pipeline templates

**Duration:** 2-8 weeks typically

**Exit Strategy:** Team becomes self-sufficient, enabling team moves to next engagement

---

## Real-World Examples

### 1. The Spotify Model (Squads, Tribes, Chapters, Guilds)

**What It Was:**
- **Squads:** Small, cross-functional teams aligned to mission (~ stream-aligned teams)
- **Tribes:** Collection of squads working on related areas (100-150 people max)
- **Chapters:** People with similar skills across squads (functional grouping for career development)
- **Guilds:** Communities of practice across the company

**What Worked:**
- ✅ Autonomy at squad level (empowered teams)
- ✅ Cross-functional teams with end-to-end ownership
- ✅ Clear mission alignment
- ✅ Chapters provided career progression and skill development
- ✅ Guilds facilitated knowledge sharing

**What Didn't Work (The Honest Truth):**
- ❌ **Not every company is Spotify** - their model evolved for their specific context
- ❌ Tribal boundaries became territorial (turf wars)
- ❌ Squads had too much autonomy → inconsistent practices, duplicated work
- ❌ Lack of platform thinking → every squad reinvented deployment, monitoring, etc.
- ❌ Chapter leads had responsibility but no authority (matrix management issues)
- ❌ Dependencies between squads still caused delays
- ❌ **Spotify itself moved away from strict model** as they scaled

**Key Lesson:** The Spotify model was a snapshot in time (2012-2014). Even Spotify evolved beyond it. Copy the principles (autonomy, alignment, cross-functional teams), not the structure.

**What to Take Away:**
- Small, autonomous, cross-functional teams aligned to value streams
- Provide platform services to reduce duplication
- Communities of practice for knowledge sharing
- Balance autonomy with alignment

---

### 2. Amazon: Two-Pizza Teams

**Model:**
- Teams should be small enough to be fed by two pizzas (~8-10 people)
- "You build it, you run it" - full ownership including on-call
- Service-oriented architecture mirrors team structure
- APIs are mandatory (all service communication through APIs)

**What Worked:**
- ✅ Small teams with clear ownership
- ✅ Service architecture enforced through team structure (Conway's Law used intentionally)
- ✅ End-to-end ownership created accountability
- ✅ Teams could move independently with well-defined interfaces
- ✅ Reduced coordination overhead

**What Was Hard:**
- ⚠️ On-call burden can be heavy for small teams
- ⚠️ Requires mature platform services (AWS itself!)
- ⚠️ Strong technical culture needed
- ⚠️ Not all work fits into two-pizza teams (infrastructure, security)

**In Team Topologies Terms:**
- Two-pizza teams = **stream-aligned teams**
- AWS internal tools/services = **platform team** capabilities
- Specialized infrastructure teams = **complicated-subsystem teams**

**Key Lesson:** Small teams with clear ownership and good boundaries scale. But you need platform services to make this work.

---

### 3. Netflix: Freedom & Responsibility

**Model:**
- Highly aligned, loosely coupled teams
- "Context, not control" - give context and trust teams to decide
- Full-cycle ownership (dev, test, deploy, operate, support)
- Strong emphasis on operational excellence
- "Paved road" philosophy - golden paths that are easy to use

**What Worked:**
- ✅ High trust and autonomy = fast innovation
- ✅ Paved roads reduce cognitive load (their internal platform)
- ✅ Context setting aligns teams without micromanagement
- ✅ Full ownership creates excellence
- ✅ Freedom to choose tools (within reason) enables best solutions

**Platform Services (Paved Road):**
- Netflix OSS (Hystrix, Eureka, Ribbon, etc.) - self-service resilience patterns
- Spinnaker - deployment pipeline as a service
- Chaos engineering tools - resilience testing
- Internal developer portal - discoverability

**In Team Topologies Terms:**
- Product teams = **stream-aligned teams** with high autonomy
- Platform teams built OSS tools = **platform team** providing X-as-a-Service
- Site reliability engineering = **enabling team** for operational excellence

**Key Lesson:** Freedom requires responsibility. High autonomy works when teams have mature practices and good platform support.

---

### 4. ThoughtWorks: Enabling Teams & Tech Radar

**Model:**
- Enabling teams are core to their consulting model
- Tech Radar - collaborative assessment of technologies (Adopt, Trial, Assess, Hold)
- Emphasis on knowledge sharing and continuous learning
- Cross-pollination between projects

**What Worked:**
- ✅ Enabling teams accelerate capability development
- ✅ Tech Radar provides organization-wide guidance
- ✅ Knowledge sharing prevents silos
- ✅ Consultants act as enabling team for clients

**In Team Topologies Terms:**
- Explicitly leverages **enabling team** pattern
- Tech Radar = tool for platform and enabling teams to align on technology choices

**Key Lesson:** Deliberately invest in capability development and knowledge sharing.

---

### 5. Other Notable Examples

**Etsy:**
- Strong focus on continuous deployment
- Everyone deploys to production (not just "ops")
- Blameless post-mortems
- Stream-aligned teams with platform services

**GitHub:**
- Small teams aligned to product areas
- "Ship to learn" culture
- Internal dogfooding (use GitHub to build GitHub)
- Platform team provides CI/CD infrastructure

**Heroku:**
- Pioneered "platform as a service" concept
- 12-factor app methodology
- Developer experience as primary focus
- Their entire business model IS a platform team

---

## Anti-Patterns to Avoid

### 1. "DevOps Team" as a Silo
- ❌ Separate team that does deployments for everyone
- ❌ Becomes a bottleneck
- ✅ **Instead:** Embed DevOps skills in stream-aligned teams, platform team provides tools

### 2. Matrix Management
- ❌ People report to multiple managers
- ❌ Unclear accountability
- ✅ **Instead:** Clear team membership, chapters/guilds for skill development (no reporting line)

### 3. Projects Over Products
- ❌ Teams formed for projects, dissolved after
- ❌ No ownership, knowledge loss
- ✅ **Instead:** Long-lived teams aligned to value streams

### 4. Too Many Dependencies
- ❌ Every feature requires 5 teams to coordinate
- ❌ Slows everything down
- ✅ **Instead:** Minimize dependencies through clear team boundaries and APIs

### 5. Platform as a Ticket System
- ❌ Platform team requires tickets for every change
- ❌ No self-service
- ✅ **Instead:** Self-service platform with X-as-a-Service model

### 6. Ignoring Cognitive Load
- ❌ Teams responsible for too many services, technologies, domains
- ❌ Quality and speed suffer
- ✅ **Instead:** Right-size team responsibilities, provide platform services to reduce load

### 7. Copying Structure Without Context
- ❌ "We'll do the Spotify model!" without understanding why
- ❌ Doesn't fit your organization's needs
- ✅ **Instead:** Understand principles, adapt to your context

---

## Applying Team Topologies to Your Azure-Native Organization

### Current State Assessment

**Questions to Ask:**
1. **What are our value streams?** (customer journeys, business capabilities)
2. **What cognitive load are teams carrying?** (too many technologies, unclear ownership)
3. **Where are the bottlenecks?** (waiting on other teams, approval gates)
4. **What platform capabilities exist?** (Bicep modules, pipeline templates)
5. **What capabilities are missing?** (what do teams repeatedly build from scratch)

---

### Example Azure Organization Structure

#### Stream-Aligned Teams (Product Teams)

**Customer Portal Team:**
- **Owns:** Customer-facing web application
- **Stack:** ASP.NET Core, React, Azure App Service, Cosmos DB
- **Consumes from Platform:** Bicep modules, pipeline templates, Azure Dev Box environments
- **Size:** 6-8 people (frontend, backend, QA)
- **Cognitive Load:** Focus on customer experience, business logic
- **Not Responsible For:** Infrastructure details, compliance config, pipeline maintenance

**Payments Team:**
- **Owns:** Payment processing services
- **Stack:** .NET 8, Azure Functions, Service Bus, SQL Database
- **Consumes from Platform:** Secure database templates, payment gateway integrations, PCI-DSS policies
- **Size:** 5-7 people
- **Cognitive Load:** Payment flows, fraud detection, integrations

**Mobile Team:**
- **Owns:** iOS and Android apps
- **Stack:** Swift, Kotlin, Azure App Center, API Management
- **Consumes from Platform:** App Center CI/CD, backend API scaffolding
- **Size:** 6-8 people (iOS, Android, QA)

**Internal Tools Team:**
- **Owns:** Admin dashboards, internal reporting, tools
- **Stack:** Blazor, Azure Static Web Apps, Power BI
- **Consumes from Platform:** Standard web hosting templates
- **Size:** 4-5 people

---

#### Platform Team

**Size:** 4-8 people (grows with number of stream-aligned teams)

**Composition:**
- Platform engineers (Bicep, PowerShell, Terraform)
- Azure specialists (networking, security, governance)
- Developer experience focus (documentation, support)

**Services Provided (X-as-a-Service):**

1. **Azure Landing Zones:**
   - Subscription vending machine
   - Pre-configured networking (VNet, NSGs, firewall rules)
   - Azure Policy baselines
   - Self-service through PowerShell or portal

2. **Bicep Module Library:**
   - Web apps (App Service with security built-in)
   - Databases (SQL, Cosmos with backup and encryption)
   - Storage accounts (private endpoints, lifecycle policies)
   - Functions, Service Bus, Key Vault
   - All modules include monitoring, security, naming conventions

3. **Azure Pipeline Templates:**
   - .NET build and test
   - Infrastructure deployment (Bicep)
   - Security scanning (Defender for DevOps)
   - Production deployment with approvals
   - Golden path: `extends: template@platform-templates`

4. **Development Environments:**
   - Azure Dev Box definitions (VS Code, Visual Studio, tools pre-installed)
   - Self-service provisioning
   - Auto-shutdown policies

5. **Observability Stack:**
   - Application Insights auto-configured
   - Standard dashboards and alerts
   - Log Analytics workspaces
   - Cost monitoring dashboards

6. **Security Baseline:**
   - Defender for Cloud enabled
   - Security policies enforced
   - Compliance dashboards
   - Remediation runbooks

**Team Topologies Interaction:**
- **Primary Mode:** X-as-a-Service (self-service modules and templates)
- **Collaboration Mode:** When designing new capabilities (e.g., new database pattern)
- **Support:** Office hours, Slack channel, but not ticket-based

**Success Metrics:**
- 80%+ of teams using platform services
- Developer NPS score > 40
- Time to provision new environment: < 1 day
- Support requests declining over time (better docs)

---

#### Enabling Team(s)

Your enabling team(s) might be part-time roles or a small dedicated team depending on size.

**Cloud & Security Enablement (2-3 people):**

**Current Focus Areas:**
- Help teams adopt Terraform for multi-cloud scenarios
- Azure governance and cost optimization
- Security best practices and threat modeling
- Defender for Cloud remediation

**Engagement Model:**
- 4-week embedded engagements with stream-aligned teams
- Workshops and pairing sessions
- Create guides and documentation
- Move to next team after knowledge transfer

**Example Engagement:**
- Payments Team needs to adopt Terraform for AWS integration
- Enabling team member embeds for 4 weeks
- Week 1: Workshop and pair on first module
- Week 2-3: Continue pairing, team takes more ownership
- Week 4: Team works independently, enabler reviews and advises
- Result: Payments Team can use Terraform independently, guide published for others

**DevOps Practices Enablement (1-2 people):**

**Focus Areas:**
- Testing strategies (unit, integration, E2E)
- Feature flags and progressive delivery
- Observability and monitoring
- Incident response and on-call practices

---

#### Complicated-Subsystem Teams (If Needed)

**Most Azure organizations won't need these**, but examples might include:

**AI/ML Platform Team (if you have significant ML workload):**
- Own model training infrastructure
- Provide simple API for stream-aligned teams to use models
- Handle complex ML engineering (feature stores, model versioning, A/B testing)

---

### How Your DevOps Engineers Fit In

From your DevOps career ladder work, here's how DevOps skills map to Team Topologies:

**Option 1: DevOps Engineers in Stream-Aligned Teams**
- Embedded with product teams
- Help team own their deployment and operations
- Build and maintain team-specific automation
- Part of the team's on-call rotation
- **Career Path:** DevOps Engineer → Senior DevOps → Team Lead / Staff Engineer

**Option 2: DevOps Engineers in Platform Team**
- Build platform services for all teams
- Create Bicep modules, pipeline templates
- Manage Azure governance and landing zones
- Focus on developer experience
- **Career Path:** Platform Engineer → Senior Platform Engineer → Staff Platform Engineer → Principal

**Option 3: DevOps Engineers in Enabling Team**
- Coach teams on DevOps practices
- Help teams adopt platform services
- Run workshops and training
- Research and evaluate new tools
- **Career Path:** DevOps Engineer → Enabling Coach → Principal Engineer (Technical Enablement)

**Recommendation:**
- **Most DevOps engineers** should be in stream-aligned teams (embedded)
- **2-4 senior DevOps engineers** in platform team (building tools)
- **1-2 staff/principal engineers** as enabling team (coaching, standards)

**What to Avoid:**
- ❌ "DevOps team" that does deployments for everyone (bottleneck)
- ❌ DevOps as ticket-based service (contradicts DevOps philosophy)

---

## Implementation Roadmap

### Phase 1: Assess (2-4 weeks)

**Activities:**
1. Map current teams and their responsibilities
2. Identify value streams
3. Document current cognitive load and pain points
4. Identify existing platform capabilities (even informal ones)
5. Survey developers on biggest bottlenecks

**Deliverables:**
- Current state diagram
- List of value streams
- Cognitive load assessment
- Gap analysis

---

### Phase 2: Design (2-4 weeks)

**Activities:**
1. Design stream-aligned team structure aligned to value streams
2. Define platform team services and roadmap
3. Identify enabling team needs
4. Define team interaction modes
5. Create transition plan

**Deliverables:**
- Future state organization design
- Platform team charter and roadmap
- Enabling team engagement model
- Team APIs and boundaries

**Key Decisions:**
- How many stream-aligned teams? (based on value streams)
- What does platform team provide? (start small, expand)
- Full-time enabling team or part-time?
- Timeline for transition

---

### Phase 3: Pilot (3-6 months)

**Start Small:**
- Form one stream-aligned team with clear boundaries
- Start building platform team (2-3 people initially)
- Pilot one platform service (e.g., Bicep module library)
- Try one enabling engagement

**Learn and Iterate:**
- Gather feedback weekly
- Adjust team boundaries if needed
- Add platform services based on demand
- Document what works

---

### Phase 4: Scale (6-12 months)

**Expand:**
- Form additional stream-aligned teams
- Grow platform team as services expand
- Formalize enabling team practices
- Build out full platform roadmap

**Measure:**
- DORA metrics per team
- Platform adoption rates
- Developer satisfaction scores
- Cognitive load reduction

---

## Measuring Success

### Team-Level Metrics

**Stream-Aligned Teams:**
- Deployment frequency (weekly → daily)
- Lead time for changes (days → hours)
- Mean time to recovery (< 1 hour)
- Change failure rate (< 15%)
- Team satisfaction scores

**Platform Team:**
- Platform service adoption rate (target: 80%+)
- Developer NPS for platform (target: 40+)
- Time to provision new service (target: < 1 day)
- Support ticket volume (trending down)
- Self-service success rate (first-time use without support)

**Enabling Team:**
- Teams successfully enabled (per quarter)
- Time to proficiency (target: < 6 weeks)
- Knowledge retention (check-ins after 3 months)
- Guides and documentation created
- Workshop satisfaction scores

### Organizational Metrics

- Overall DORA metrics trending up
- Cross-team dependencies decreasing
- Innovation time increasing (less toil)
- Incident frequency decreasing
- Employee engagement/retention improving

---

## Key Takeaways

1. **Team structure determines architecture** (Conway's Law) - design it intentionally
2. **Cognitive load is the constraint** - reduce extraneous load through platform services
3. **Four team types:** Stream-aligned (most teams), Platform (internal product), Enabling (coaches), Complicated-subsystem (rare)
4. **Three interaction modes:** X-as-a-Service (default), Collaboration (temporary), Facilitating (enabling)
5. **Platform teams are product teams** - focus on self-service and developer experience
6. **Don't copy models blindly** - understand principles, adapt to your context
7. **Start small and iterate** - pilot with one team, learn, then scale
8. **Measure and adapt** - use metrics to validate organizational changes

---

## Further Reading

**Books:**
- *Team Topologies* by Matthew Skelton and Manuel Pais (THE source)
- *Accelerate* by Forsgren, Humble, Kim (research backing Team Topologies)
- *The DevOps Handbook* by Gene Kim et al.

**Articles:**
- Team Topologies website: https://teamtopologies.com
- ThoughtWorks Tech Radar: https://www.thoughtworks.com/radar
- Spotify Engineering Blog (for historical context)

**Your Related Resources:**
- [Platform Engineering & Developer Experience](platform-engineering-devex.md)
- [DevOps Career Ladder](devops-career-ladder.md)
- [Platform Engineering for Azure](platform-engineering-azure.md)
- [Delegation](../leadership/delegation.md) - how to empower teams
- [Stakeholder Management](../leadership/stakeholder-management.md) - managing across team boundaries

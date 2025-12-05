# Product Requirements Document: AVISPL AI-Powered Service Management Enhancement

**Version:** 1.0
**Date:** December 5, 2025
**Product Owner:** Chris Clancy, ServiceNow AI Foundry
**Stakeholders:** AVISPL Service Management Team

---

## 1. Problem Statement

AVISPL's service delivery organization faces significant operational challenges that impact service efficiency, customer satisfaction, and resource utilization:

- **Manual Case Triage & Research**: Case managers spend 4-6 hours manually enriching case information, researching equipment documentation across multiple systems (ServiceNow, SharePoint/SDCS, manufacturer websites), and determining appropriate support pathways.

- **Knowledge Fragmentation**: Critical technical knowledge is dispersed across ServiceNow (1000+ legacy articles), SharePoint sites, manufacturer documentation, and tribal knowledge. Knowledge creation is inconsistent and infrequent, limiting institutional learning.

- **Inefficient Field Dispatch**: Field technicians experience approximately 30% return visits due to insufficient preparation, skills mismatch, or incomplete contextual information. Average dispatch time is 4 hours, with technicians often starting troubleshooting from scratch.

- **Limited Remote Resolution**: Only ~50% of non-Symphony cases achieve remote resolution despite 70% of all cases being potentially remotely resolvable. Manual processes limit the ability to scale remote support capabilities.

- **Resource Capacity Constraints**: Manual processes create bottlenecks in case management queues (TSR/TSE teams) and limit the organization's ability to handle the approximately 15,000 monthly cases efficiently.

These challenges result in extended resolution times, increased operational costs (unnecessary truck rolls), diminished customer satisfaction, and underutilization of available technical resources.

---

## 2. Goals and Objectives

### Qualitative Goals
- **Empower Service Teams**: Provide AI-assisted tools that augment human decision-making rather than replace expertise
- **Improve Customer Experience**: Reduce resolution times and increase first-contact resolution rates
- **Enable Knowledge Continuity**: Capture and leverage institutional knowledge systematically
- **Accelerate Remote Resolution**: Increase the proportion of cases resolved without field dispatch

### Measurable Objectives
- **Increase Remote Resolution Rate**: From 50% to 60-70% for non-Symphony cases within 6 months
- **Reduce Case Triage Time**: From 4-6 hours to under 2 hours for case information enrichment
- **Improve First Visit Resolution**: From 70% to 80% for field dispatches requiring on-site service
- **Reduce Average Dispatch Duration**: From 4 hours to 2 hours through better preparation and context
- **Increase Knowledge Article Creation**: From ad-hoc to 80% of resolved cases generating knowledge candidates
- **Reduce Return Visits**: Decrease "ran out of time" and "insufficient information" return visit causes by 40%

---

## 3. User Personas

### Case Manager / TSR (Technical Support Representative)
**Role**: Front-line case triage and administrative support
**Motivations**: Process cases efficiently, ensure accurate information, route to appropriate resources
**Pain Points**: Manual data entry, hunting for contract information, unclear customer entitlements
**Context**: Handles global queue, processes all incoming cases before assignment

### TSE (Technical Support Engineer)
**Role**: Remote technical troubleshooting and resolution
**Motivations**: Solve customer problems quickly, avoid escalations, build technical expertise
**Pain Points**: Scattered documentation, limited SDCS access efficiency, repetitive research tasks
**Context**: Needs access to equipment specs, troubleshooting guides, historical case data

### Field Service Technician
**Role**: On-site technical resolution
**Motivations**: First-visit resolution, efficient site visits, clear work instructions
**Pain Points**: Arriving on-site without adequate context, skills mismatch, redundant troubleshooting
**Context**: Mobile workforce requiring comprehensive pre-visit briefing and historical context

### Dispatch Manager
**Role**: Work order assignment and field resource coordination
**Motivations**: Optimal resource utilization, skills-based routing, minimize travel time
**Pain Points**: Manual skills matching, geographic optimization, incomplete case context
**Context**: Manages regional technician teams with varying skill sets

### Knowledge Manager
**Role**: Knowledge base curation and governance
**Motivations**: Maintain knowledge quality, encourage contribution, ensure discoverability
**Pain Points**: Low contribution rates, inconsistent formatting, outdated content
**Context**: Loosely defined process, limited resources for active curation

---

## 4. Use Cases

### UC-1: AI-Assisted Case Enrichment
**Actor**: Case Manager (TSR)
**Scenario**: A case arrives via email describing "podium panel not working" at a customer site. The Case Manager uses AI to automatically populate contract information, identify the specific room configuration from SDCS, retrieve equipment models, and suggest initial support pathway based on customer entitlement.
**Outcome**: Case information complete in under 30 minutes instead of 4-6 hours

### UC-2: Remote Troubleshooting Intelligence
**Actor**: TSE (Technical Support Engineer)
**Scenario**: An Extron podium panel issue is assigned to a TSE. The AI agent automatically retrieves the specific model from SDCS documentation (CAD drawings, bill of materials), searches manufacturer troubleshooting guides, reviews historical case resolutions for the same location/equipment, and generates a prioritized troubleshooting plan with step-by-step instructions.
**Outcome**: TSE has comprehensive troubleshooting guide within minutes, increasing likelihood of remote resolution

### UC-3: Intelligent Field Dispatch Coordination
**Actor**: Dispatch Manager
**Scenario**: A case requires on-site service. The AI agent analyzes required skills (based on equipment type and problem description), evaluates field technician locations, availability, and skill matrices, and recommends the optimal technician. It also generates a comprehensive work order summary including historical context, previous resolution notes, and specific equipment documentation.
**Outcome**: Right technician dispatched with complete context, increasing first-visit resolution

### UC-4: Automated Knowledge Generation
**Actor**: TSE or Field Technician
**Scenario**: Upon case closure, the AI reviews resolution notes, problem description, troubleshooting steps, and equipment details to auto-generate a draft knowledge article. The article is presented to the resolver for review/approval before entering the knowledge workflow.
**Outcome**: 80% of cases generate knowledge candidates with minimal human effort

### UC-5: Major Case Pattern Detection
**Actor**: Case Manager / TSE
**Scenario**: Multiple cases arrive describing similar symptoms for a specific device model. The AI agent identifies the pattern, suggests creating or associating with a major/parent case, and auto-links related child cases.
**Outcome**: Faster identification of widespread issues, reduced redundant troubleshooting

### UC-6: Proactive Alert Case Resolution
**Actor**: System (automated)
**Scenario**: Symphony generates an alert for device latency. The AI agent automatically accesses the customer environment, performs initial diagnostic checks, determines if the issue self-resolved, and either auto-closes the case or escalates with diagnostic context.
**Outcome**: Reduced manual intervention on Symphony-generated cases (currently 70% of volume)

---

## 5. Key Features

### Priority 1: Remote Troubleshooting Agent
**Purpose**: Aggregate multi-source data to provide comprehensive troubleshooting guidance
**Capabilities**:
- Query SDCS SharePoint for as-built CAD drawings and bills of materials
- Search ServiceNow case history for location/equipment patterns
- Index and retrieve manufacturer documentation (Extron, Polycom, etc.)
- Generate prioritized troubleshooting steps based on problem description
- Present visual documentation (network diagrams, schematics) with contextual analysis
- Suggest remote vs. on-site resolution pathway

### Priority 2: Knowledge Generation Assistant
**Purpose**: Reduce friction in knowledge article creation
**Capabilities**:
- Auto-draft knowledge articles from resolution notes
- Extract key information: problem, solution, equipment, steps
- Format content for AI consumption (simple, structured)
- Route to knowledge approval workflow
- Track knowledge coverage gaps

### Priority 3: Dispatch Coordinator Agent
**Purpose**: Optimize field service assignment and preparation
**Capabilities**:
- Evaluate technician skills, location, and availability
- Match case requirements to technician capabilities
- Generate comprehensive work order summaries
- Include historical case context for the location
- Highlight equipment-specific documentation
- Aggregate upstream troubleshooting attempts

### Priority 4: Case Queue Intelligence (AWA Enhancement)
**Purpose**: Intelligent case assignment for remote support teams
**Capabilities**:
- Auto-populate case contract and contact information
- Route based on account relationships (e.g., dedicated Polycom team)
- Balance workload across available agents
- Consider skills, capacity, and case complexity
- Auto-suggest major case associations for known issues

### Priority 5: AI Assistant for Agent Personas
**Purpose**: Provide in-context assistance within ServiceNow
**Capabilities**:
- Answer procedural questions ("How do I create a quote?")
- Access knowledge base and SharePoint how-to documentation
- Provide equipment-specific guidance
- Suggest next-best actions based on case state

---

## 6. Success Metrics

### Operational Efficiency
- **Case Triage Time**: Average time from case creation to "information complete" status
- **Remote Resolution Rate**: Percentage of cases closed without field dispatch
- **Field Dispatch Duration**: Average time spent on-site per work order task
- **Queue Wait Time**: Average time cases spend in assignment queues

### Quality Metrics
- **First Visit Resolution Rate**: Percentage of dispatches resolved on first visit
- **Return Visit Causes**: Distribution of reasons for incomplete work orders
- **Knowledge Article Creation Rate**: Articles generated per 100 closed cases
- **Major Case Detection Time**: Time to identify and associate related cases

### User Adoption
- **Agent Usage Frequency**: Daily interactions with AI assistant
- **Troubleshooting Agent Utilization**: Percentage of eligible cases using remote agent
- **Knowledge Approval Rate**: Percentage of AI-drafted articles approved/published
- **User Satisfaction Score**: Agent feedback on AI tool usefulness (1-5 scale)

### Business Impact
- **Cost per Case**: Total operational cost divided by cases resolved
- **Truck Roll Avoidance Rate**: Cases resolved remotely vs. historical dispatch rate
- **Customer Satisfaction (CSAT)**: Survey scores post-resolution
- **Mean Time to Resolution (MTTR)**: Average time from case creation to closure

---

## 7. Assumptions

### Technical Assumptions
- ServiceNow evaluation instance remains accessible and stable
- SDCS SharePoint can be accessed via external content connectors or dev tenant
- Field service skills matrix population will be completed for technicians
- Symphony alert integration continues to generate cases as structured data
- Manufacturer websites (Extron, Polycom, etc.) are publicly accessible for indexing

### Process Assumptions
- Case managers will continue manual queue-based assignment during AWA configuration
- Knowledge approval workflows exist and can accommodate increased article volume
- Field technicians will document resolution notes consistently
- TSE/TSR teams have reliable access to customer environments for remote troubleshooting

### Organizational Assumptions
- Leadership support for AI adoption and change management
- Users are willing to trial new AI capabilities with feedback loops
- IT security team will collaborate on SharePoint integration requirements
- Change adoption will be gradual given organizational culture (acknowledged slow adoption)

### Data Assumptions
- Historical case resolution notes contain sufficient detail for knowledge generation
- SDCS folder structure is consistent (e.g., folder 95 contains schematics)
- Skills data for remote support teams will be captured in ServiceNow in 2026
- Current case volume (~15,000/month) remains stable

---

## 8. Timeline

### Phase 1: Foundation & Quick Wins (Weeks 1-4)
- **Week 1-2**: Environment setup, data access validation (SDCS dev tenant)
- **Week 2-3**: Deploy knowledge generation AI skill (out-of-box)
- **Week 3-4**: Index external manufacturer content (Extron, Polycom)
- **Deliverable**: Functional knowledge generation on case closure

### Phase 2: Remote Troubleshooting Agent (Weeks 5-8)
- **Week 5-6**: Configure external content connectors for SDCS SharePoint
- **Week 6-7**: Build remote troubleshooting agent with multi-source queries
- **Week 7-8**: Test with sample cases, refine data sources
- **Deliverable**: Remote troubleshooting agent providing aggregated guidance

### Phase 3: Dispatch & Assignment Intelligence (Weeks 9-12)
- **Week 9-10**: Configure AWA for field service with skills-based routing
- **Week 10-11**: Build dispatch coordinator agent for work order generation
- **Week 11-12**: Test assignment workflows and summarization
- **Deliverable**: Intelligent dispatch with contextual work orders

### Phase 4: Evaluation & Iteration (Weeks 13-16)
- **Week 13-14**: User acceptance testing with TSE/TSR/field tech personas
- **Week 14-15**: Gather feedback, refine agent behaviors
- **Week 15-16**: Document findings, create production deployment plan
- **Deliverable**: Production readiness assessment and roadmap

### Future Enhancements (Post-Initial Sprint)
- Knowledge hygiene agent (Q2 2026 alignment)
- WhatsApp/Chat integrations
- PMV (Preventive Maintenance Visit) automation
- Alert/event management intelligence
- Advanced AWA for remote support team (with skills capture)

---

## 9. Stakeholders

### Core Team
- **Phil Caiazzo**: Service Operations Lead (AVISPL) - Decision authority, process owner
- **Mike Dennis**: Field Service Manager (AVISPL) - Field operations, technician experience
- **Aaron Seiden**: ServiceNow Platform Owner (AVISPL) - Technical implementation, integrations
- **Peter Wychunis**: Case Operations Lead (AVISPL) - Day-to-day workflows, process details
- **Chris Clancy**: AI Foundry Lead (ServiceNow) - Solution architect, implementation lead

### Extended Stakeholders
- **Keith Wachunas**: Operations Team Member (AVISPL) - Detailed workflow input
- **Mike Buckner**: ServiceNow Account Team - Strategic guidance, best practices
- **IT Security Team** (AVISPL): SharePoint integration approval and configuration
- **TSE/TSR Teams**: End users, feedback providers, adoption champions
- **Field Service Technicians**: End users, work order quality validation
- **Knowledge Management Team**: Article review and approval workflow owners

### Informed Parties
- **AVISPL Executive Leadership**: Budget approval, change management support
- **ServiceNow Product Teams**: Feature feedback, platform capabilities input

---

## 10. Known Constraints or Dependencies

### Technical Constraints
- **SharePoint Access**: SDCS production environment contains sensitive data (pricing, credentials). Requires either:
  - Dev tenant with sanitized sample data, or
  - Folder-level path restrictions (e.g., only folder 95 with schematics)
- **Skills Data Availability**: Remote support skills matrix not yet in ServiceNow (2026 initiative)
- **Instance Limitations**: Evaluation POC instance may have performance or data retention limits
- **External Content Indexing**: Rate limits and access restrictions on manufacturer websites

### Organizational Dependencies
- **IT Approval Cycles**: SharePoint connector configuration requires IT DevOps team involvement
- **Change Management**: Slow organizational adoption requires careful rollout and champion engagement
- **Resource Availability**: Core stakeholder time for testing and feedback during sprint
- **Knowledge Process Maturity**: Formal knowledge workflow being defined (starting Feb 2026)

### Data Quality Dependencies
- **Resolution Notes Consistency**: Variable quality of existing case resolution documentation
- **SDCS Standardization**: Folder structure and document placement consistency varies
- **Alert Data Structure**: Symphony alert quality and actionability
- **Contract Data Accuracy**: Entitlement and service agreement information completeness

### Process Dependencies
- **AWA Implementation**: Field service AWA in progress; remote support AWA not yet started
- **Skills Capture**: Field service skills populated; remote support skills pending
- **Knowledge Approval Workflow**: Exists but loosely defined and infrequently used
- **Case Assignment Logic**: Currently manual queue-based; AWA transition in progress

### Timeline Risks
- **Security Approval Delays**: IT security review of SharePoint integration could extend timeline
- **User Availability**: Testing cycles may conflict with peak service periods
- **Data Access Lag**: Delays in provisioning dev tenant or folder access
- **Scope Creep**: Stakeholder enthusiasm may drive additional feature requests mid-sprint

---

## Open Questions

1. **SDCS Access Model**: Will AVISPL provide a dev tenant with sample data, or configure folder-level access restrictions in production SharePoint?

2. **Skills Timeline**: When will remote support (TSE/TSR) skills be captured in ServiceNow, and can partial data enable pilot testing?

3. **Knowledge Approval Authority**: Who will review and approve AI-generated knowledge articles during the pilot? Is additional reviewer capacity needed?

4. **Symphony Alert Prioritization**: Should AI agent handle all Symphony alerts, or focus on specific device types/alert categories initially?

5. **Major Case Workflow**: Does a formal major/parent case process exist today, or does this need to be defined as part of the build?

6. **User Feedback Mechanism**: How should TSE/TSR/field tech feedback be collected during pilot (surveys, interviews, embedded feedback)?

7. **Production Deployment Approval**: What criteria must be met for production deployment post-pilot (metrics, stakeholder sign-off, security review)?

8. **Integration with BKR/D365**: Are external connectors for Beaker (BKR) or Dynamics 365 (D365) systems in scope for future phases?

9. **Multi-Language Support**: Are there requirements for non-English support given global service delivery teams?

10. **Performance Expectations**: What are acceptable response times for AI agent queries (e.g., troubleshooting plan generation, case enrichment)?

---

## Risks

### High-Impact Risks

**Risk**: SharePoint integration blocked by IT security
**Impact**: Cannot access SDCS documentation, limiting remote troubleshooting agent value
**Mitigation**:
- Engage IT security early with clear use case and data governance plan
- Prepare alternative: use small sample dataset manually uploaded to ServiceNow
- Demonstrate security controls (folder-level access, audit logging)

**Risk**: Low user adoption due to organizational change resistance
**Impact**: Tools unused, no measurable business outcomes
**Mitigation**:
- Identify early adopter champions within TSE/TSR teams
- Focus on high-value, low-friction use cases first (knowledge generation)
- Provide hands-on training and celebrate quick wins publicly
- Gather and act on user feedback rapidly

**Risk**: Poor data quality yields inaccurate AI outputs
**Impact**: User distrust, tool abandonment
**Mitigation**:
- Start with high-quality data sources (manufacturer sites, structured alerts)
- Implement human-in-the-loop validation for critical decisions
- Provide transparency on data sources and confidence levels
- Establish feedback loops to flag and correct errors

### Medium-Impact Risks

**Risk**: AWA implementation delays impact dispatch coordinator agent
**Impact**: Cannot demonstrate skills-based intelligent routing
**Mitigation**:
- Focus Phase 3 on work order summarization independent of AWA
- Use manual assignment with AI-enhanced context as interim solution
- Align timeline with AVISPL's AWA deployment schedule

**Risk**: Knowledge approval process bottleneck
**Impact**: AI generates articles faster than they can be reviewed/published
**Mitigation**:
- Implement auto-approval for high-confidence articles with post-publication review
- Provide bulk review UI for knowledge managers
- Start with small volume during pilot to calibrate review capacity

**Risk**: Scope creep from stakeholder feature requests
**Impact**: Timeline overrun, core features incomplete
**Mitigation**:
- Maintain prioritized backlog with clear MVP definition
- Defer non-critical features to "Future Enhancements"
- Require formal change control for mid-sprint scope additions

**Risk**: Insufficient SDCS sample data for realistic testing
**Impact**: Cannot validate remote troubleshooting agent effectiveness
**Mitigation**:
- Define minimum viable dataset early (10-15 sample jobs with CAD/BOM)
- Work with Mike Dennis team to identify representative use cases
- Supplement with manufacturer documentation indexing to demonstrate pattern

---

## Appendix: Supporting Materials

- **Workshop Transcript**: ServiceNow AI Foundry & AVISPL Process Walk & Use Case Workshop (December 2025)
- **Client Ideas Document**: Possible AI Agent Considerations (AVISPL)
- **ServiceNow Instance**: Evaluation POC environment (provisioned)
- **Process Diagrams**: Case Management and Dispatch workflows (referenced)
- **Knowledge Article White Paper**: AI-Optimized Knowledge Design (ServiceNow, to be shared)

---

**Document Prepared By**: AI Assistant (Claude Code)
**Review Status**: Draft for Stakeholder Review
**Next Steps**: Circulate for feedback, schedule kickoff meeting, initiate Phase 1 environment setup

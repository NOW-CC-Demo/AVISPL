# AVISPL AI Agents - Visual Diagram Specifications
**Purpose:** Detailed specifications for creating presentation visuals
**Tools:** PowerPoint, Lucidchart, Draw.io, or Visio
**Version:** 1.0
**Date:** December 5, 2025

---

## Table of Contents
1. [Architecture Diagrams](#architecture-diagrams)
2. [Workflow Flow Diagrams](#workflow-flow-diagrams)
3. [Data Integration Diagrams](#data-integration-diagrams)
4. [User Interface Mockups](#user-interface-mockups)
5. [Metrics Dashboards](#metrics-dashboards)
6. [Color Palette & Branding](#color-palette--branding)

---

## 1. Architecture Diagrams

### Diagram 1.1: AVISPL Agent Ecosystem Overview

**Purpose:** High-level view of the multi-agent system

**Layout:** Hierarchical pyramid structure

**Elements:**

```
┌─────────────────────────────────────────────────────────────────┐
│                    AVISPL Agentic AI Platform                    │
│                     (ServiceNow Yokohama)                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────────────────────────────────────────────┐    │
│  │         Master Orchestrator Agent                       │    │
│  │                                                         │    │
│  │  • Case Intake Analysis                                 │    │
│  │  • Workflow Routing Decisions                           │    │
│  │  • Agent Team Coordination                              │    │
│  │                                                         │    │
│  └───────────────┬────────────────────────────────────────┘    │
│                  │                                               │
│                  │ (Routing Logic)                               │
│                  │                                               │
│     ┌────────────┼────────────┬─────────────┬─────────────┐    │
│     │            │             │             │             │    │
│  ┌──▼──────┐ ┌──▼───────┐ ┌──▼───────┐ ┌──▼───────┐ ┌──▼────┐│
│  │ PRIO 1  │ │  PRIO 2  │ │  PRIO 3  │ │  PRIO 4  │ │ PRIO5 ││
│  │         │ │          │ │          │ │          │ │       ││
│  │ Remote  │ │Knowledge │ │ Dispatch │ │  Queue   │ │ Agent ││
│  │ Trouble-│ │Generation│ │Coordin-  │ │ Intel-   │ │Assist ││
│  │ shooting│ │          │ │ator      │ │ ligence  │ │       ││
│  │         │ │          │ │          │ │          │ │       ││
│  │ 5 Agents│ │ 3 Agents │ │ 3 Agents │ │ 3 Agents │ │1 Agent││
│  └─────────┘ └──────────┘ └──────────┘ └──────────┘ └───────┘│
│                                                                  │
├──────────────────────────────────────────────────────────────────┤
│                     Data Integration Layer                       │
│                                                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│  │ServiceNow│  │   SDCS   │  │Manufactu-│  │ Symphony │       │
│  │   Case   │  │SharePoint│  │rer Docs  │  │  Alerts  │       │
│  │ History  │  │          │  │          │  │          │       │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘       │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Master Orchestrator:** Large rounded rectangle, gradient fill (blue), icon: brain/network
- **Priority Agent Boxes:** Medium rectangles, different colors per priority
  - Priority 1: Teal (#009999)
  - Priority 2: Purple (#6B46C1)
  - Priority 3: Orange (#F97316)
  - Priority 4: Green (#10B981)
  - Priority 5: Blue (#3B82F6)
- **Data Layer:** Smaller rounded rectangles, light gray (#E5E7EB), database icons
- **Arrows:** Solid lines with arrowheads showing data flow
- **Background:** Light gradient from white to light blue

**PowerPoint Instructions:**
1. Insert shape: Rounded Rectangle for main container
2. Use SmartArt "Hierarchy" for agent structure
3. Add icons from PowerPoint icon library (brain, database, network)
4. Group elements for easy repositioning

---

### Diagram 1.2: Orchestrator-Worker-Communicator Pattern (Priority 1 Detail)

**Purpose:** Show agent team collaboration for troubleshooting workflow

**Layout:** Swim lane horizontal flow

**Elements:**

```
┌─────────────────────────────────────────────────────────────────────┐
│ PRIORITY 1: REMOTE TROUBLESHOOTING AGENT TEAM                       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│ ┌──────────────────────────────────────────────────────────────┐   │
│ │ ORCHESTRATOR:  Troubleshooting Coordinator                    │   │
│ │ • Analyzes case context                                       │   │
│ │ • Plans troubleshooting strategy                              │   │
│ │ • Coordinates data retrieval                                  │   │
│ └────────────────┬─────────────────────────────────────────────┘   │
│                  │                                                   │
│                  │ (Delegates to Workers)                            │
│                  │                                                   │
│     ┌────────────┼────────────┬──────────────┐                     │
│     │            │             │              │                     │
│  ┌──▼────────┐ ┌▼──────────┐ ┌▼───────────┐ │                     │
│  │ WORKER 1  │ │ WORKER 2  │ │  WORKER 3  │ │                     │
│  │           │ │           │ │            │ │                     │
│  │   SDCS    │ │Manufactu- │ │   Case     │ │                     │
│  │ Retrieval │ │rer Docs   │ │  History   │ │                     │
│  │           │ │ Specialist│ │  Analyst   │ │                     │
│  │           │ │           │ │            │ │                     │
│  └───────────┘ └───────────┘ └────────────┘ │                     │
│       │              │              │         │                     │
│       │              │              │         │                     │
│       └──────────────┴──────────────┴─────────┘                     │
│                      │                                               │
│                      │ (Aggregated Results)                          │
│                      │                                               │
│  ┌───────────────────▼─────────────────────────────────────┐       │
│  │ COMMUNICATOR: Troubleshooting Guide Presenter            │       │
│  │ • Synthesizes findings from all workers                  │       │
│  │ • Creates actionable step-by-step plan                   │       │
│  │ • Presents to TSE in Now Assist Panel                    │       │
│  └──────────────────────────────────────────────────────────┘       │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Orchestrator Box:** Large rounded rectangle, teal gradient, icon: coordinator/planner
- **Worker Boxes:** Medium rectangles, lighter teal, icons: document/search/chart
- **Communicator Box:** Large rounded rectangle, dark teal, icon: presentation/chat
- **Arrows:** Dotted lines for delegation, solid bold lines for data flow
- **Background:** White with subtle teal accent on left border

**PowerPoint Instructions:**
1. Use SmartArt "Process" type
2. Customize colors to match teal theme
3. Add labels for each agent role
4. Include small icons for visual interest

---

## 2. Workflow Flow Diagrams

### Diagram 2.1: Remote Troubleshooting Workflow (Detailed)

**Purpose:** End-to-end workflow from case assignment to outcome

**Layout:** Vertical flowchart with decision branches

**Elements:**

```
        ┌────────────────────────────────────┐
        │    START: Case Assigned to TSE     │
        │   OR Manual "Get AI Plan" Click    │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │   Flow Action: Input Validation    │
        │   • Location present?               │
        │   • Equipment info available?       │
        │   • TSE has access?                 │
        └────────────────┬───────────────────┘
                         │
                         ▼
                     [Pass?]────────No────▶ [Error: Request More Info]
                         │
                        Yes
                         │
                         ▼
        ┌────────────────────────────────────┐
        │   Orchestrator Agent Activation    │
        │   • Analyze problem description     │
        │   • Determine data sources needed   │
        │   • Assess complexity               │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │    PARALLEL WORKER EXECUTION       │
        │                                    │
        │  ┌──────────┐  ┌──────────┐       │
        │  │  SDCS    │  │Manufactu-│       │
        │  │Retrieval │  │rer Docs  │       │
        │  └─────┬────┘  └────┬─────┘       │
        │        │            │              │
        │        │    ┌───────▼────┐         │
        │        │    │    Case    │         │
        │        │    │  History   │         │
        │        │    └───────┬────┘         │
        │        └────────────┤              │
        │                     │              │
        └─────────────────────┬──────────────┘
                              │
                              ▼
        ┌────────────────────────────────────┐
        │  Flow Action: Aggregate Results    │
        │  • Collect all worker outputs       │
        │  • Handle partial failures          │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │   Communicator Agent Synthesis     │
        │   • Generate troubleshooting plan   │
        │   • Prioritize steps                │
        │   • Include visual docs             │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │  Now Assist Panel: Display to TSE  │
        │  • Show plan with action buttons    │
        │  • [Start] [Not Helpful] [Report]  │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │   TSE Executes Troubleshooting     │
        │   • Follows step-by-step plan       │
        │   • Documents outcomes              │
        └────────────────┬───────────────────┘
                         │
                         ▼
                  [Outcome?]
                     /   |   \
                    /    |    \
           Remote  /     |     \ Escalate
          Success /      |      \ to Field
                 /       |       \
                ▼        ▼        ▼
            [Close]  [Attempt] [Create
             Case    More Steps] Work Order]
                         │
                         ▼
        ┌────────────────────────────────────┐
        │  Capture Outcome & Feedback        │
        │  • Record resolution type           │
        │  • Collect feedback rating          │
        │  • Update learning pipeline         │
        └────────────────┬───────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │    END: Case Updated               │
        └────────────────────────────────────┘
```

**Visual Styling:**
- **Start/End:** Rounded rectangles, green (start), red (end)
- **Process Steps:** Rectangles, light blue fill
- **Agent Steps:** Rectangles, teal fill with agent icon
- **Decision Points:** Diamond shapes, yellow fill
- **Parallel Execution:** Grouped box with dotted border
- **Arrows:** Solid black, labeled for decision branches
- **Background:** White

**PowerPoint Instructions:**
1. Use flowchart shapes from Insert > Shapes
2. Align shapes using PowerPoint alignment tools
3. Use connectors for arrows (they snap to shape edges)
4. Color code by step type (agent vs. flow action vs. decision)
5. Add shadow effects to agent boxes for emphasis

---

### Diagram 2.2: Knowledge Generation Workflow (Simplified)

**Purpose:** Show automated knowledge article creation process

**Layout:** Horizontal swim lane with user interaction points

**Elements:**

```
┌──────────────────────────────────────────────────────────────────┐
│ KNOWLEDGE GENERATION WORKFLOW                                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│ TRIGGER: Case State = "Resolved" or "Closed"                     │
│                                                                   │
│  ┌─────────┐     ┌──────────┐     ┌──────────┐     ┌─────────┐ │
│  │  Case   │────▶│Evaluate  │────▶│ Generate │────▶│ Human   │ │
│  │ Closes  │     │Knowledge │     │ Article  │     │ Review  │ │
│  │         │     │Worthiness│     │  Draft   │     │         │ │
│  └─────────┘     └──────────┘     └──────────┘     └────┬────┘ │
│                       │                                   │      │
│                       │ [Score]                           │      │
│                       │                                   │      │
│              ┌────────┼────────┐                          │      │
│              │        │        │                          │      │
│           [High]   [Medium]  [Low]                        │      │
│              │        │        │                          │      │
│              │        │        └──▶ Skip                  │      │
│              │        │                                   │      │
│              │        └──▶ Prompt User ──┐               │      │
│              │                           │               │      │
│              └──────────────┬────────────┘               │      │
│                             │                            │      │
│                             └──▶ Auto-Generate ──────────┘      │
│                                                          │      │
│                                           [User Action]  │      │
│                                                 /   |    \       │
│                                          Approve Edit  Reject   │
│                                               /    |     \       │
│                                              /     |      \      │
│  ┌─────────┐                                /      |       \     │
│  │ Submit  │◀─────────────────────────────┘       │        └──▶│
│  │   to    │◀──────────────────────────────────────┘             │
│  │Knowledge│                                                     │
│  │Workflow │                                                     │
│  └─────────┘                                                     │
│      │                                                           │
│      ▼                                                           │
│  [Published to Knowledge Base]                                  │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Process Boxes:** Rounded rectangles, purple theme
- **Evaluation Step:** Diamond shape with score labels
- **Human Review:** Yellow box with user icon
- **Decision Branches:** Arrows labeled with actions
- **End State:** Green rounded rectangle
- **Background:** Light purple gradient

**PowerPoint Instructions:**
1. Use SmartArt "Process" with customization
2. Add decision diamond for score branching
3. Highlight human review step with different color
4. Use icons: checkbox (approve), pencil (edit), X (reject)

---

## 3. Data Integration Diagrams

### Diagram 3.1: Data Sources Connected to AI Platform

**Purpose:** Show all data sources feeding the AI agents

**Layout:** Hub-and-spoke model

**Elements:**

```
                      ┌─────────────────────┐
                      │                     │
                      │  ServiceNow AI      │
                      │  Agent Platform     │
                      │  (Yokohama)         │
                      │                     │
                      └──────────┬──────────┘
                                 │
                 ┌───────────────┼───────────────┐
                 │               │               │
     ┌───────────▼────────┐      │      ┌───────▼────────────┐
     │  ServiceNow Case   │      │      │   SDCS SharePoint  │
     │     History        │      │      │                    │
     │                    │      │      │  • CAD Drawings    │
     │  • 15K cases/month │      │      │  • BOMs            │
     │  • Resolution notes│      │      │  • Schematics      │
     │  • Historical data │      │      │  • Network diagrams│
     │                    │      │      │                    │
     │  Type: RAG         │      │      │  Type: External    │
     │  Retriever         │      │      │  Content Connector │
     └────────────────────┘      │      └────────────────────┘
                                 │
                 ┌───────────────┼───────────────┐
                 │               │               │
     ┌───────────▼────────┐      │      ┌───────▼────────────┐
     │  Manufacturer      │      │      │ Contract Management│
     │  Documentation     │      │      │     System         │
     │                    │      │      │                    │
     │  • Extron guides   │      │      │  • Customer        │
     │  • Polycom support │      │      │    contracts       │
     │  • Crestron docs   │      │      │  • Entitlements    │
     │                    │      │      │  • SLA terms       │
     │  Type: Web Crawler │      │      │                    │
     │  + Retriever       │      │      │  Type: REST API    │
     └────────────────────┘      │      └────────────────────┘
                                 │
                                 │
                         ┌───────▼────────┐
                         │   Symphony     │
                         │     Alerts     │
                         │                │
                         │  • Device      │
                         │    monitoring  │
                         │  • Structured  │
                         │    alert data  │
                         │                │
                         │  Type: Direct  │
                         │  Integration   │
                         └────────────────┘
```

**Visual Styling:**
- **Central Hub:** Large hexagon, blue gradient, AI icon in center
- **Data Source Boxes:** Rounded rectangles, different colors per type:
  - ServiceNow: Blue (#3B82F6)
  - SharePoint: Green (#10B981)
  - Manufacturer: Orange (#F97316)
  - Contract System: Purple (#8B5CF6)
  - Symphony: Red (#EF4444)
- **Connection Lines:** Bidirectional arrows showing data flow
- **Labels:** Integration type below each box
- **Icons:** Database, document, web, API icons
- **Background:** Radial gradient from white (center) to light gray (edges)

**PowerPoint Instructions:**
1. Insert hexagon shape for central hub
2. Arrange data source boxes in circle around hub
3. Use connector lines (Insert > Shapes > Lines > Connector)
4. Add icons from PowerPoint icon library
5. Group all elements for easy resizing

---

### Diagram 3.2: SDCS SharePoint Security Architecture

**Purpose:** Show folder-level access control for sensitive data

**Layout:** Layered security model

**Elements:**

```
┌───────────────────────────────────────────────────────────────┐
│  AVISPL SDCS SharePoint Security Architecture                 │
├───────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────────────────────────────────────────────┐     │
│  │        SDCS SharePoint Site                          │     │
│  │                                                       │     │
│  │  ┌────────────────────────────────────────────────┐  │     │
│  │  │  FOLDER 95: Schematics & Diagrams (ACCESSIBLE)│  │     │
│  │  │                                                 │  │     │
│  │  │  ✓ CAD drawings                                │  │     │
│  │  │  ✓ Network diagrams                            │  │     │
│  │  │  ✓ Equipment layouts                           │  │     │
│  │  │  ✓ Public technical documentation              │  │     │
│  │  │                                                 │  │     │
│  │  │  AI Agent Access: ALLOWED                      │  │     │
│  │  └────────────────────────────────────────────────┘  │     │
│  │                                                       │     │
│  │  ┌────────────────────────────────────────────────┐  │     │
│  │  │  OTHER FOLDERS: Contracts, Pricing (RESTRICTED)│  │     │
│  │  │                                                 │  │     │
│  │  │  ✗ Customer contracts                          │  │     │
│  │  │  ✗ Pricing information                         │  │     │
│  │  │  ✗ Credentials                                 │  │     │
│  │  │  ✗ Sensitive customer data                     │  │     │
│  │  │                                                 │  │     │
│  │  │  AI Agent Access: BLOCKED                      │  │     │
│  │  └────────────────────────────────────────────────┘  │     │
│  └─────────────────────────────────────────────────────┘     │
│                                                               │
│  ┌─────────────────────────────────────────────────────┐     │
│  │     Security Controls Applied                        │     │
│  │                                                       │     │
│  │  🔒 OAuth 2.0 Authentication                         │     │
│  │  🔒 Folder-Level Path Restrictions                   │     │
│  │  🔒 PII Detection & Masking (Sensitive Data Handler) │     │
│  │  🔒 Audit Logging (All Access Tracked)               │     │
│  │  🔒 Read-Only Permissions (No Write/Delete)          │     │
│  └─────────────────────────────────────────────────────┘     │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **SharePoint Site:** Large rounded rectangle, light blue background
- **Folder 95 (Accessible):** Green box with checkmarks
- **Restricted Folders:** Red box with X marks
- **Security Controls:** Gray box with lock icons
- **Icons:** Green checkmarks for allowed, red X for blocked, lock for security
- **Background:** White with subtle blue gradient

**PowerPoint Instructions:**
1. Use nested rectangles to show hierarchy
2. Color code: Green = accessible, Red = restricted
3. Add lock icons for security controls
4. Use callout shapes for annotations

---

## 4. User Interface Mockups

### Mockup 4.1: Now Assist Panel - Troubleshooting Plan Display

**Purpose:** Show how TSE views AI-generated troubleshooting plan

**Layout:** Simulated ServiceNow Now Assist Panel

**Elements:**

```
┌──────────────────────────────────────────────────────────────┐
│ Now Assist                                     [Close] [Help] │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  AI Troubleshooting Plan                          🤖       │
│  ─────────────────────────────────────────────────────────   │
│                                                              │
│  📋 EQUIPMENT CONTEXT                                         │
│  ────────────────────────────────────────────────────────    │
│  Model: Extron DMP 128 Plus AT                              │
│  Location: Building A, Room 205 (Conference Room)           │
│  Network: VLAN 100, Switch Port 12                          │
│  [📄 View Network Diagram]                                   │
│                                                              │
│  🔧 TROUBLESHOOTING STEPS (Prioritized)                      │
│  ────────────────────────────────────────────────────────    │
│                                                              │
│  ☐ Step 1: Verify power and connections (5 min)            │
│     • Check power LED is illuminated                        │
│     • Verify all input cables securely connected            │
│     • Expected Outcome: All connection LEDs green           │
│     📘 Reference: Extron DMP 128 Quick Start Guide          │
│                                                              │
│  ☐ Step 2: Test input signal switching (10 min)            │
│     • Use front panel to switch between inputs              │
│     • Verify each input source displays correctly           │
│     • Expected Outcome: All 4 inputs functional             │
│     📘 Reference: Case #CS0045123 (similar resolution)      │
│                                                              │
│  ☐ Step 3: Check firmware version (5 min)                  │
│     • Access web interface (IP from diagram)                │
│     • Navigate to System > Firmware                         │
│     • Expected Outcome: v2.05 or newer                      │
│     📘 Reference: Extron Firmware Bulletin 2024-03          │
│                                                              │
│  ⚠️  DECISION POINT                                           │
│  ────────────────────────────────────────────────────────    │
│  • If Steps 1-3 resolve issue → Document and close case    │
│  • If Steps 1-3 fail → Escalate to field dispatch          │
│                                                              │
│  📊 HISTORICAL CONTEXT                                        │
│  ────────────────────────────────────────────────────────    │
│  Similar cases: 8 cases in last 6 months                    │
│  Remote resolution rate: 75% (6 of 8)                       │
│  Common resolution: Firmware update + input reconfiguration │
│                                                              │
│  📚 ADDITIONAL RESOURCES                                      │
│  ────────────────────────────────────────────────────────    │
│  [📄 SDCS Schematic - Room 205]                              │
│  [📖 Extron DMP 128 Troubleshooting Guide]                  │
│  [📋 Past Case: CS0045123]                                   │
│                                                              │
│  ──────────────────────────────────────────────────────────  │
│                                                              │
│  [▶️ Start Troubleshooting]  [👎 Not Helpful]  [⚠️ Report]  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Panel Background:** Light gray (#F3F4F6)
- **Section Headers:** Bold, dark gray with icons
- **Steps:** Checkboxes (empty), numbered list
- **Expected Outcomes:** Italicized, indented
- **References:** Blue hyperlinks with book icon
- **Decision Point:** Yellow background box with warning icon
- **Buttons:** Bottom bar with distinct colors:
  - Start: Green (#10B981)
  - Not Helpful: Orange (#F97316)
  - Report: Red (#EF4444)
- **Icons:** Emoji-style for visual interest

**PowerPoint Instructions:**
1. Create rounded rectangle for panel frame
2. Use text boxes for content sections
3. Insert icons from PowerPoint icon library
4. Add button shapes with rounded corners at bottom
5. Use subtle drop shadow for 3D effect

---

### Mockup 4.2: Mobile Work Order Briefing (Field Technician View)

**Purpose:** Show mobile-optimized briefing interface

**Layout:** Mobile phone screen mockup (vertical orientation)

**Elements:**

```
┌─────────────────────────────────┐
│  ⬅️  Work Order #WO0012345      │ (Header Bar - Dark Blue)
├─────────────────────────────────┤
│                                 │
│  📸 [Site Photo Placeholder]    │ (Visual Header)
│                                 │
├─────────────────────────────────┤
│                                 │
│  ⚡ QUICK FACTS                 │ (Always Visible Section)
│                                 │
│  📍 Marriott Convention Center  │
│      123 Main St, Boston MA     │
│      [🗺️ Navigate]              │
│                                 │
│  🔧 Extron DMP 128 Plus AT      │
│  Issue: No signal to projector  │
│  Priority: ⭐⭐⭐ High            │
│  Est. Time: 2-3 hours           │
│                                 │
├─────────────────────────────────┤
│                                 │
│  ▶️ Problem Details             │ (Expandable - Collapsed)
│                                 │
│  ▼ Already Tried ✅             │ (Expandable - Expanded)
│                                 │
│     Remote TSE Actions:         │
│     ✓ Verified power connections│
│     ✓ Tested input switching    │
│     ✓ Checked firmware (v2.03)  │
│     ✗ Issue persists            │
│                                 │
│     ⏱️ Attempted: Dec 5, 2:30pm │
│                                 │
│  ▶️ Recommended Approach        │ (Expandable - Collapsed)
│                                 │
│  ▶️ Documentation              │ (Expandable - Collapsed)
│                                 │
├─────────────────────────────────┤
│                                 │ (Action Bar - Sticky Bottom)
│  [⬇️ Download Offline PDF]     │
│                                 │
│  [▶️ Start Work Order]          │ (Large Green Button)
│                                 │
└─────────────────────────────────┘
```

**Visual Styling:**
- **Header Bar:** Dark blue (#1E40AF), white text
- **Site Photo:** Placeholder with camera icon
- **Quick Facts:** White background, bold labels
- **Expandable Sections:** Light gray background, collapse/expand arrows
- **Already Tried Section:** Green checkmarks for completed, red X for failed
- **Action Buttons:** Full-width, bottom sticky bar
  - Download: Light blue, cloud icon
  - Start: Green (#10B981), large and prominent
- **Icons:** Clear, high-contrast for mobile visibility
- **Font Size:** Large for readability (16px+ body text)

**PowerPoint Instructions:**
1. Insert phone frame shape (rounded rectangle with black border)
2. Create sections as separate text boxes
3. Use collapse/expand arrows (▶️/▼) to indicate interaction
4. Make buttons large and touch-friendly (44px+ height)
5. Add subtle shadow to phone frame for depth

---

## 5. Metrics Dashboards

### Dashboard 5.1: Business Impact Metrics (Executive View)

**Purpose:** High-level KPI dashboard for leadership

**Layout:** 4-quadrant dashboard with big numbers

**Elements:**

```
┌──────────────────────────────────────────────────────────────────┐
│  AVISPL AI Agents - Business Impact Dashboard       [Q4 2025]   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────────┐  ┌────────────────────┐                 │
│  │  CASE TRIAGE TIME  │  │ REMOTE RESOLUTION  │                 │
│  │                    │  │       RATE         │                 │
│  │       2.1          │  │                    │                 │
│  │      hours         │  │        64%         │                 │
│  │                    │  │                    │                 │
│  │  ▼ 58% reduction   │  │  ▲ 28% increase    │                 │
│  │  vs. baseline      │  │  vs. baseline      │                 │
│  │                    │  │                    │                 │
│  │  ━━━━━━━━━━━━━━━━  │  │  ━━━━━━━━━━━━━━━━  │                 │
│  │  Target: <2 hours  │  │  Target: 60-70%    │                 │
│  │  Status: ✅ ON TRACK│  │  Status: ✅ ACHIEVED│                 │
│  └────────────────────┘  └────────────────────┘                 │
│                                                                  │
│  ┌────────────────────┐  ┌────────────────────┐                 │
│  │  FIRST-VISIT       │  │  KNOWLEDGE ARTICLE │                 │
│  │   RESOLUTION       │  │  GENERATION RATE   │                 │
│  │                    │  │                    │                 │
│  │       78%          │  │       9,234        │                 │
│  │                    │  │    articles/month  │                 │
│  │  ▲ 11% improvement │  │                    │                 │
│  │  vs. baseline      │  │  ▲ 923% increase   │                 │
│  │                    │  │  vs. baseline      │                 │
│  │  ━━━━━━━━━━━━━━━━  │  │  ━━━━━━━━━━━━━━━━  │                 │
│  │  Target: 80%       │  │  Target: 12K/month │                 │
│  │  Status: 🟡 PROGRESS│  │  Status: 🟡 PROGRESS│                 │
│  └────────────────────┘  └────────────────────┘                 │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  FINANCIAL IMPACT (Estimated Annual)                     │   │
│  │                                                           │   │
│  │  💰 Truck Roll Avoidance:        $950,000               │   │
│  │  💰 Labor Efficiency Gains:      $720,000               │   │
│  │  💰 Customer Retention Value:    $180,000               │   │
│  │  ─────────────────────────────────────────               │   │
│  │  💰 Total Annual Value:          $1,850,000             │   │
│  │                                                           │   │
│  │  ROI: 627%  |  Payback Period: 2.3 months              │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  TREND: Case Volume vs. Resolution Efficiency            │   │
│  │                                                           │   │
│  │  15.5K ┤                    ╭────────● Cases Handled     │   │
│  │  15.0K ┤              ╭─────╯                             │   │
│  │  14.5K ┤        ╭─────╯                                   │   │
│  │  14.0K ┤  ╭─────╯                                         │   │
│  │        ├───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───     │   │
│  │        Jul Aug Sep Oct Nov Dec Jan Feb Mar Apr May Jun   │   │
│  │                                                           │   │
│  │  Resolution Rate:  50% → 52% → 56% → 60% → 64%           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Quadrant Boxes:** White background, subtle shadow, rounded corners
- **Big Numbers:** Large font (48-72px), bold, color-coded:
  - Green: On track/achieved
  - Yellow: In progress
  - Red: At risk (if applicable)
- **Trend Indicators:** Arrows (▲ green for improvement, ▼ red for decline)
- **Status Badges:** Colored emoji (✅ green, 🟡 yellow, 🔴 red)
- **Financial Section:** Light green background, dollar icons
- **Trend Chart:** Simple line chart, blue line with dots
- **Background:** Light gray (#F9FAFB)

**PowerPoint Instructions:**
1. Use 2x2 grid layout for quadrants
2. Insert large text boxes for big numbers
3. Use PowerPoint chart feature for trend line
4. Add colored shape behind status text for emphasis
5. Use icons (💰, ✅) for visual interest

---

### Dashboard 5.2: Agent Performance Metrics (Operational View)

**Purpose:** Detailed agent execution metrics for operations team

**Layout:** Table + bar charts

**Elements:**

```
┌──────────────────────────────────────────────────────────────────┐
│  Agent Execution Performance - Last 30 Days           [Dec 2025]│
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  AGENT UTILIZATION & SUCCESS RATES                               │
│  ───────────────────────────────────────────────────────────────│
│                                                                  │
│  Agent Name              Executions  Avg Time  Success  User    │
│                                                  Rate    Rating  │
│  ──────────────────────────────────────────────────────────────  │
│  Remote Troubleshooting    4,234     4.2 min     94%    4.3/5.0 │
│  ████████████████████████████░░░░░░░░░░░░░░░░░░░░               │
│                                                                  │
│  Knowledge Generation     11,567     1.8 min     87%    4.1/5.0 │
│  ████████████████████████████████████████░░░░░░░                 │
│                                                                  │
│  Dispatch Coordinator        892     3.5 min     91%    4.5/5.0 │
│  ████████████████████░░░░░░░░░░░░░░░░░░░░░░░░░░                 │
│                                                                  │
│  Case Enrichment         14,123     0.9 min     96%    4.2/5.0 │
│  ██████████████████████████████████████████████                  │
│                                                                  │
│  AI Assistant             2,845     0.3 min     89%    4.4/5.0 │
│  ████████████████████████░░░░░░░░░░░░░░░░░░░░░░                 │
│                                                                  │
│  ──────────────────────────────────────────────────────────────  │
│  TOTAL                   33,661     1.9 min     91%    4.3/5.0 │
│                                                                  │
│  ───────────────────────────────────────────────────────────────│
│                                                                  │
│  TOKEN USAGE & COST EFFICIENCY                                   │
│  ───────────────────────────────────────────────────────────────│
│                                                                  │
│  Total Tokens Used: 248.3M tokens                                │
│  Average per Execution: 7,375 tokens                             │
│  Estimated Cost: $18,624                                         │
│  Cost per Case: $1.24                                            │
│                                                                  │
│  ↓ 12% reduction in avg tokens vs. previous month               │
│                                                                  │
│  ───────────────────────────────────────────────────────────────│
│                                                                  │
│  TOP FEEDBACK THEMES (User Comments Analysis)                    │
│  ───────────────────────────────────────────────────────────────│
│                                                                  │
│  ✅ Positive (87%)                                               │
│     • "Saved me 30+ minutes of research"                        │
│     • "Exactly what I needed, step-by-step"                     │
│     • "Found documentation I didn't know existed"               │
│                                                                  │
│  ⚠️  Improvement Opportunities (13%)                             │
│     • "Some steps were redundant" (3% of feedback)              │
│     • "Needed more equipment images" (6% of feedback)           │
│     • "Plan took too long to generate" (4% of feedback)         │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Visual Styling:**
- **Table:** Alternating row colors (white/light gray)
- **Bar Charts:** Horizontal bars showing volume, color gradient (blue to green)
- **Success Rate:** Color-coded (>90% green, 80-90% yellow, <80% red)
- **User Ratings:** Star icons filled proportionally
- **Metrics Summary:** Large numbers, bold font
- **Feedback Themes:** Checkmark (✅) for positive, warning (⚠️) for opportunities
- **Background:** White with section dividers in gray

**PowerPoint Instructions:**
1. Create table using PowerPoint table feature
2. Add horizontal bar charts using PowerPoint chart feature
3. Use conditional formatting colors for success rates
4. Insert star icons for ratings
5. Use callout boxes for key metrics

---

## 6. Color Palette & Branding

### AVISPL + ServiceNow Brand Colors

**Primary Colors:**

```
ServiceNow Green: #62D84E
ServiceNow Blue:  #1B3454
AVISPL Teal:      #009999
AVISPL Navy:      #003366
```

**Agent Priority Colors (for diagrams):**

```
Priority 1 (Troubleshooting):  #009999 (Teal)
Priority 2 (Knowledge):        #8B5CF6 (Purple)
Priority 3 (Dispatch):         #F97316 (Orange)
Priority 4 (Queue Intel):      #10B981 (Green)
Priority 5 (Assistant):        #3B82F6 (Blue)
```

**Status Colors:**

```
Success/On Track:    #10B981 (Green)
In Progress/Warning: #F59E0B (Yellow/Amber)
Error/At Risk:       #EF4444 (Red)
Neutral/Info:        #6B7280 (Gray)
```

**Background Colors:**

```
Light Background:    #F9FAFB
Medium Background:   #E5E7EB
Dark Background:     #1F2937
```

**Text Colors:**

```
Primary Text:   #111827 (Near Black)
Secondary Text: #6B7280 (Gray)
Accent Text:    #009999 (AVISPL Teal)
```

---

## PowerPoint Template Recommendations

**Slide Master Settings:**
- **Font:** Arial or Segoe UI (clean, professional)
- **Heading Size:** 28-32pt
- **Body Text Size:** 18-20pt (for readability)
- **Line Spacing:** 1.2-1.5 for body text

**Slide Layouts to Create:**
1. **Title Slide:** Logo placement, gradient background
2. **Section Divider:** Large text, minimal elements
3. **Content Slide:** Title + 2-column layout
4. **Diagram Slide:** Title + large content area
5. **Metrics Slide:** Title + 2x2 or 3x1 grid

**Animation Guidelines:**
- **Use sparingly:** Only for progressive disclosure
- **Timing:** 0.3-0.5 seconds (fast, professional)
- **Types:** Fade, Appear (avoid flashy effects)
- **Sequence:** Build content logically (top to bottom, left to right)

---

## Icon Library Recommendations

**Suggested Icon Packs (PowerPoint compatible):**
- **Microsoft PowerPoint Icons** (built-in, Insert > Icons)
- **Flaticon** (free and premium options)
- **Font Awesome** (can be inserted as shapes)
- **Noun Project** (high-quality, professional)

**Key Icons Needed:**
- Brain/AI: Orchestrator agents
- Network: Data connections
- Document: Knowledge articles
- Tools: Troubleshooting
- Person: User personas
- Shield: Security
- Chart: Analytics
- Checkmark: Success
- Warning: Attention items

---

**Document Version:** 1.0
**Last Updated:** December 5, 2025
**Status:** Ready for Visual Design Team

**Instructions for Design Team:**
1. Use this document as specification for creating PowerPoint slides
2. Apply AVISPL/ServiceNow branding consistently
3. Ensure all diagrams are scalable (vector format preferred)
4. Create template once, reuse for consistency
5. Export final presentation to PDF for distribution

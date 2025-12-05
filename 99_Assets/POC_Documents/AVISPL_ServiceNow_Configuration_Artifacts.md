# AVISPL AI Agents - ServiceNow Configuration Artifacts
**Version:** 1.0
**Date:** December 5, 2025
**Platform:** ServiceNow Yokohama Release
**Instance:** AVISPL Evaluation POC

---

## Table of Contents
1. [Agent Configuration Specifications](#agent-configuration-specifications)
2. [Flow Diagrams & Workflows](#flow-diagrams--workflows)
3. [Integration Hub Connections](#integration-hub-connections)
4. [Data Model Extensions](#data-model-extensions)
5. [Retriever Configurations](#retriever-configurations)
6. [Now Assist Panel Components](#now-assist-panel-components)
7. [Skills & AI Model Configurations](#skills--ai-model-configurations)
8. [Security & Access Controls](#security--access-controls)

---

## 1. Agent Configuration Specifications

### 1.1 Priority 1: Remote Troubleshooting Agent Team

#### Agent: AVISPL_Troubleshooting_Orchestrator_Agent

```json
{
  "name": "AVISPL_Troubleshooting_Orchestrator_Agent",
  "type": "orchestrator",
  "description": "Analyzes technical support cases and coordinates multi-source troubleshooting plan generation",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.3,
  "max_tokens": 4000,
  "tools": [
    {
      "type": "flow_action",
      "name": "Get_Case_Details",
      "sys_id": "flow_action_get_case_details"
    },
    {
      "type": "flow_action",
      "name": "Extract_Equipment_Information",
      "sys_id": "flow_action_extract_equipment"
    },
    {
      "type": "subflow",
      "name": "Identify_Similar_Historical_Cases",
      "sys_id": "subflow_historical_case_search"
    },
    {
      "type": "script",
      "name": "Parse_Problem_Description_NLP",
      "sys_id": "script_nlp_problem_parser"
    },
    {
      "type": "skill",
      "name": "Classification_Problem_Category",
      "sys_id": "skill_problem_classifier"
    }
  ],
  "instructions": "You are the Troubleshooting Orchestrator for AVISPL service cases...",
  "guardrails": {
    "content_filtering": true,
    "pii_detection": true,
    "response_validation": true
  },
  "escalation_criteria": [
    "Equipment model ambiguous",
    "Safety hazard detected",
    "100% historical field dispatch rate"
  ]
}
```

#### Agent: AVISPL_SDCS_Retrieval_Worker_Agent

```json
{
  "name": "AVISPL_SDCS_Retrieval_Worker_Agent",
  "type": "worker",
  "description": "Retrieves site-specific technical documentation from SharePoint SDCS",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.2,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "retriever",
      "name": "SDCS_SharePoint_Retriever",
      "sys_id": "retriever_sdcs_sharepoint",
      "config": {
        "external_content_source": "sharepoint_sdcs_connector",
        "search_scope": "folder_95_schematics",
        "max_results": 10,
        "relevance_threshold": 0.75
      }
    },
    {
      "type": "script",
      "name": "Parse_CAD_Drawing_Metadata",
      "sys_id": "script_cad_metadata_parser"
    },
    {
      "type": "integration",
      "name": "SharePoint_Document_Fetch_API",
      "sys_id": "integration_sharepoint_api"
    },
    {
      "type": "flow_action",
      "name": "Extract_Network_Topology",
      "sys_id": "flow_action_network_topology"
    }
  ],
  "instructions": "You are the SDCS Documentation Specialist...",
  "timeout_seconds": 120,
  "retry_policy": {
    "max_retries": 2,
    "backoff_strategy": "exponential"
  }
}
```

#### Agent: AVISPL_Manufacturer_Doc_Worker_Agent

```json
{
  "name": "AVISPL_Manufacturer_Doc_Worker_Agent",
  "type": "worker",
  "description": "Retrieves manufacturer troubleshooting guides and technical specifications",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.2,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "retriever",
      "name": "Extron_Knowledge_Base_Retriever",
      "sys_id": "retriever_extron_kb",
      "config": {
        "external_content_source": "extron_website_connector",
        "max_results": 8,
        "relevance_threshold": 0.70
      }
    },
    {
      "type": "retriever",
      "name": "Polycom_Support_Retriever",
      "sys_id": "retriever_polycom_support",
      "config": {
        "external_content_source": "polycom_website_connector",
        "max_results": 8,
        "relevance_threshold": 0.70
      }
    },
    {
      "type": "ai_search",
      "name": "Manufacturer_Semantic_Search",
      "sys_id": "ai_search_manufacturer_docs"
    }
  ],
  "instructions": "You are the Manufacturer Documentation Expert...",
  "timeout_seconds": 90
}
```

#### Agent: AVISPL_Case_History_Worker_Agent

```json
{
  "name": "AVISPL_Case_History_Worker_Agent",
  "type": "worker",
  "description": "Analyzes similar historical cases to identify resolution patterns",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.3,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "retriever",
      "name": "ServiceNow_Case_History_Retriever",
      "sys_id": "retriever_case_history",
      "config": {
        "table": "sn_customerservice_case",
        "filters": "state=resolved^ORstate=closed",
        "max_results": 15,
        "relevance_threshold": 0.65
      }
    },
    {
      "type": "skill",
      "name": "Similarity_Analysis",
      "sys_id": "skill_similarity_analysis"
    },
    {
      "type": "script",
      "name": "Calculate_Resolution_Success_Patterns",
      "sys_id": "script_resolution_patterns"
    },
    {
      "type": "flow_action",
      "name": "Get_Resolution_Notes_By_Location",
      "sys_id": "flow_action_location_cases"
    }
  ],
  "instructions": "You are the Historical Case Pattern Analyst..."
}
```

#### Agent: AVISPL_Troubleshooting_Communicator_Agent

```json
{
  "name": "AVISPL_Troubleshooting_Communicator_Agent",
  "type": "communicator",
  "description": "Synthesizes multi-source findings into actionable troubleshooting plans",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.4,
  "max_tokens": 5000,
  "tools": [
    {
      "type": "skill",
      "name": "Summarization_Technical_Documentation",
      "sys_id": "skill_tech_summarization"
    },
    {
      "type": "skill",
      "name": "Generation_Step_By_Step_Instructions",
      "sys_id": "skill_instruction_generation"
    },
    {
      "type": "flow_action",
      "name": "Format_Troubleshooting_Plan",
      "sys_id": "flow_action_format_plan"
    },
    {
      "type": "now_assist_panel",
      "name": "Display_To_TSE",
      "sys_id": "now_assist_troubleshooting_panel"
    },
    {
      "type": "script",
      "name": "Generate_Visual_Documentation_Links",
      "sys_id": "script_visual_doc_links"
    }
  ],
  "instructions": "You are the Troubleshooting Communication Specialist...",
  "output_format": "structured_plan"
}
```

---

### 1.2 Priority 2: Knowledge Generation Agent Team

#### Agent: AVISPL_Knowledge_Evaluation_Orchestrator_Agent

```json
{
  "name": "AVISPL_Knowledge_Evaluation_Orchestrator_Agent",
  "type": "orchestrator",
  "description": "Evaluates resolved cases for knowledge article worthiness",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Haiku",
  "temperature": 0.2,
  "max_tokens": 2000,
  "tools": [
    {
      "type": "skill",
      "name": "Classification_Knowledge_Worthiness",
      "sys_id": "skill_knowledge_classifier",
      "config": {
        "categories": ["high", "medium", "low"],
        "threshold_high": 0.80,
        "threshold_medium": 0.50
      }
    },
    {
      "type": "script",
      "name": "Calculate_Case_Reusability_Score",
      "sys_id": "script_reusability_score"
    },
    {
      "type": "flow_action",
      "name": "Get_Resolution_Notes_Quality",
      "sys_id": "flow_action_resolution_quality"
    },
    {
      "type": "retriever",
      "name": "Check_Existing_Knowledge_Coverage",
      "sys_id": "retriever_knowledge_dedup"
    }
  ],
  "instructions": "You are the Knowledge Worthiness Evaluator...",
  "decision_outputs": {
    "high": "auto_generate",
    "medium": "prompt_user",
    "low": "skip"
  }
}
```

#### Agent: AVISPL_Knowledge_Content_Worker_Agent

```json
{
  "name": "AVISPL_Knowledge_Content_Worker_Agent",
  "type": "worker",
  "description": "Drafts knowledge articles from case resolution data",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.5,
  "max_tokens": 4000,
  "tools": [
    {
      "type": "skill",
      "name": "Generation_Knowledge_Article",
      "sys_id": "skill_kb_generation",
      "config": {
        "template": "avispl_kb_article_template",
        "format": "ai_optimized"
      }
    },
    {
      "type": "skill",
      "name": "Summarization_Technical_Content",
      "sys_id": "skill_tech_summarization"
    },
    {
      "type": "script",
      "name": "Extract_Steps_From_Resolution_Notes",
      "sys_id": "script_step_extractor"
    },
    {
      "type": "flow_action",
      "name": "Format_For_AI_Consumption",
      "sys_id": "flow_action_ai_format"
    }
  ],
  "instructions": "You are the Knowledge Article Drafter...",
  "output_validation": {
    "required_fields": ["title", "problem", "symptoms", "resolution_steps"],
    "max_length": 5000,
    "format": "markdown"
  }
}
```

#### Agent: AVISPL_Knowledge_Review_Communicator_Agent

```json
{
  "name": "AVISPL_Knowledge_Review_Communicator_Agent",
  "type": "communicator",
  "description": "Coordinates human review and approval of AI-generated articles",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Haiku",
  "temperature": 0.3,
  "max_tokens": 2000,
  "tools": [
    {
      "type": "now_assist_panel",
      "name": "Article_Review_Interface",
      "sys_id": "now_assist_kb_review_panel"
    },
    {
      "type": "flow_action",
      "name": "Submit_To_Knowledge_Workflow",
      "sys_id": "flow_action_kb_workflow"
    },
    {
      "type": "skill",
      "name": "Generation_Suggested_Edits",
      "sys_id": "skill_edit_suggestions"
    },
    {
      "type": "integration",
      "name": "Send_Review_Notification",
      "sys_id": "integration_email_notification"
    }
  ],
  "instructions": "You are the Knowledge Review Coordinator...",
  "review_options": ["approve", "edit", "reject", "defer"],
  "reminder_schedule": "24_hours"
}
```

---

### 1.3 Priority 3: Dispatch Coordinator Agent Team

#### Agent: AVISPL_Dispatch_Strategy_Orchestrator_Agent

```json
{
  "name": "AVISPL_Dispatch_Strategy_Orchestrator_Agent",
  "type": "orchestrator",
  "description": "Optimizes field technician assignment using skills-based routing",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.3,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "skill",
      "name": "Classification_Required_Skills",
      "sys_id": "skill_skills_classifier",
      "config": {
        "skill_categories": ["equipment_expertise", "technical_skills", "certifications"]
      }
    },
    {
      "type": "flow_action",
      "name": "Get_Available_Field_Technicians",
      "sys_id": "flow_action_get_technicians"
    },
    {
      "type": "script",
      "name": "Calculate_Travel_Distance_Matrix",
      "sys_id": "script_distance_calculator"
    },
    {
      "type": "subflow",
      "name": "Check_Technician_Schedule_Capacity",
      "sys_id": "subflow_schedule_check"
    }
  ],
  "instructions": "You are the Dispatch Strategy Coordinator...",
  "scoring_weights": {
    "skills_match": 0.40,
    "travel_time": 0.30,
    "workload": 0.20,
    "historical_performance": 0.10
  },
  "recommendation_count": 3
}
```

#### Agent: AVISPL_Work_Order_Context_Worker_Agent

```json
{
  "name": "AVISPL_Work_Order_Context_Worker_Agent",
  "type": "worker",
  "description": "Compiles comprehensive work order briefings for field technicians",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.3,
  "max_tokens": 4000,
  "tools": [
    {
      "type": "retriever",
      "name": "ServiceNow_Case_History_Retriever",
      "sys_id": "retriever_case_history"
    },
    {
      "type": "flow_action",
      "name": "Get_Upstream_Troubleshooting_Notes",
      "sys_id": "flow_action_upstream_notes"
    },
    {
      "type": "retriever",
      "name": "SDCS_SharePoint_Retriever",
      "sys_id": "retriever_sdcs_sharepoint"
    },
    {
      "type": "skill",
      "name": "Summarization_Multi_Case_Timeline",
      "sys_id": "skill_timeline_summary"
    }
  ],
  "instructions": "You are the Work Order Context Specialist...",
  "output_sections": [
    "case_summary",
    "problem_history",
    "troubleshooting_attempted",
    "equipment_info",
    "site_context",
    "technical_docs",
    "recommended_actions",
    "parts_suggestions"
  ]
}
```

#### Agent: AVISPL_Technician_Briefing_Communicator_Agent

```json
{
  "name": "AVISPL_Technician_Briefing_Communicator_Agent",
  "type": "communicator",
  "description": "Delivers mobile-optimized work order briefings to field technicians",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Haiku",
  "temperature": 0.3,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "now_assist_panel",
      "name": "Mobile_Briefing_Panel",
      "sys_id": "now_assist_mobile_briefing",
      "config": {
        "platform": "mobile",
        "offline_mode": true
      }
    },
    {
      "type": "integration",
      "name": "Send_Mobile_Notification",
      "sys_id": "integration_mobile_push"
    },
    {
      "type": "skill",
      "name": "Summarization_Mobile_Optimized",
      "sys_id": "skill_mobile_summary"
    },
    {
      "type": "flow_action",
      "name": "Generate_Offline_Briefing_PDF",
      "sys_id": "flow_action_pdf_generator"
    }
  ],
  "instructions": "You are the Field Technician Briefing Coordinator...",
  "mobile_optimization": {
    "max_sections": 6,
    "expandable_content": true,
    "visual_priority": true
  }
}
```

---

### 1.4 Priority 4: Queue Intelligence Agent Team

#### Agent: AVISPL_Queue_Assignment_Orchestrator_Agent

```json
{
  "name": "AVISPL_Queue_Assignment_Orchestrator_Agent",
  "type": "orchestrator",
  "description": "Intelligent case routing to TSE/TSR teams with workload balancing",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.2,
  "max_tokens": 2500,
  "tools": [
    {
      "type": "integration",
      "name": "AWA_Configuration_API",
      "sys_id": "integration_awa_api"
    },
    {
      "type": "skill",
      "name": "Classification_Case_Complexity",
      "sys_id": "skill_complexity_classifier",
      "config": {
        "categories": ["simple_tsr", "medium_tse", "complex_senior_tse"]
      }
    },
    {
      "type": "flow_action",
      "name": "Get_Available_TSE_Capacity",
      "sys_id": "flow_action_tse_capacity"
    },
    {
      "type": "script",
      "name": "Calculate_Workload_Balance_Score",
      "sys_id": "script_workload_balancer"
    },
    {
      "type": "retriever",
      "name": "Account_Relationship_Retriever",
      "sys_id": "retriever_account_relationships"
    }
  ],
  "instructions": "You are the Case Queue Assignment Strategist...",
  "awa_integration": {
    "assignment_group": "TSE_Support_Team",
    "capacity_threshold": 8,
    "balance_tolerance": 0.30
  }
}
```

#### Agent: AVISPL_Case_Enrichment_Worker_Agent

```json
{
  "name": "AVISPL_Case_Enrichment_Worker_Agent",
  "type": "worker",
  "description": "Auto-populates case fields with contract, contact, and entitlement data",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Haiku",
  "temperature": 0.1,
  "max_tokens": 2000,
  "tools": [
    {
      "type": "integration",
      "name": "Contract_Management_System_API",
      "sys_id": "integration_contract_mgmt"
    },
    {
      "type": "retriever",
      "name": "Customer_Account_Retriever",
      "sys_id": "retriever_customer_accounts"
    },
    {
      "type": "script",
      "name": "Parse_Email_Contact_Information",
      "sys_id": "script_email_parser"
    },
    {
      "type": "flow_action",
      "name": "Validate_Service_Entitlement",
      "sys_id": "flow_action_entitlement_check"
    }
  ],
  "instructions": "You are the Case Enrichment Specialist...",
  "enrichment_fields": [
    "account_name",
    "account_number",
    "contract_status",
    "service_tier",
    "primary_contact",
    "equipment_covered",
    "sla_terms"
  ]
}
```

#### Agent: AVISPL_Assignment_Notification_Communicator_Agent

```json
{
  "name": "AVISPL_Assignment_Notification_Communicator_Agent",
  "type": "communicator",
  "description": "Notifies TSEs of case assignments with enriched context",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Haiku",
  "temperature": 0.3,
  "max_tokens": 2000,
  "tools": [
    {
      "type": "now_assist_panel",
      "name": "Assignment_Notification_Panel",
      "sys_id": "now_assist_assignment_panel"
    },
    {
      "type": "integration",
      "name": "Send_Email_Notification",
      "sys_id": "integration_email_notification"
    },
    {
      "type": "skill",
      "name": "Summarization_Case_Snapshot",
      "sys_id": "skill_case_summary"
    },
    {
      "type": "flow_action",
      "name": "Generate_Quick_Reference_Card",
      "sys_id": "flow_action_ref_card"
    }
  ],
  "instructions": "You are the Assignment Notification Coordinator...",
  "notification_triggers": {
    "in_app_always": true,
    "email_high_priority": true,
    "email_vip_customer": true
  }
}
```

---

### 1.5 Priority 5: AI Assistant Agent

#### Agent: AVISPL_Context_Assistant_Orchestrator_Agent

```json
{
  "name": "AVISPL_Context_Assistant_Orchestrator_Agent",
  "type": "orchestrator",
  "description": "Conversational AI assistant for procedural and equipment questions",
  "scope": "x_avispl_ai_agents",
  "active": true,
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.4,
  "max_tokens": 3000,
  "tools": [
    {
      "type": "skill",
      "name": "Classification_Question_Type",
      "sys_id": "skill_question_classifier",
      "config": {
        "categories": ["procedural", "equipment", "troubleshooting", "policy"]
      }
    },
    {
      "type": "retriever",
      "name": "ServiceNow_Knowledge_Base_Retriever",
      "sys_id": "retriever_sn_kb"
    },
    {
      "type": "retriever",
      "name": "SharePoint_How_To_Documentation_Retriever",
      "sys_id": "retriever_sharepoint_howto"
    },
    {
      "type": "retriever",
      "name": "Equipment_Technical_Specs_Retriever",
      "sys_id": "retriever_equipment_specs"
    },
    {
      "type": "now_assist_panel",
      "name": "Chat_Interface",
      "sys_id": "now_assist_chat_panel"
    }
  ],
  "instructions": "You are the AVISPL AI Assistant...",
  "conversation_config": {
    "max_turns": 10,
    "context_retention": true,
    "source_citations": "required"
  }
}
```

---

## 2. Flow Diagrams & Workflows

### 2.1 Remote Troubleshooting Agentic Workflow

```
Workflow: Remote_Troubleshooting_Agentic_Workflow
Sys ID: workflow_remote_troubleshooting
Table: sn_customerservice_case
Trigger: Case assigned to TSE queue OR Manual "Get AI Troubleshooting Plan" button

┌─────────────────────────────────────────────────────────────┐
│ START: Case Assigned to TSE / Manual Trigger               │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Flow Action: Input_Validation                               │
│ - Check location field populated                            │
│ - Check equipment information present                       │
│ - Validate TSE has access permissions                       │
│ Output: validation_passed (true/false)                      │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼ [validation_passed = true]
┌─────────────────────────────────────────────────────────────┐
│ Agent: AVISPL_Troubleshooting_Orchestrator_Agent            │
│ Input: case_sys_id, case_number, problem_description        │
│ Output: data_retrieval_plan (object)                        │
│   - sdcs_needed: boolean                                    │
│   - manufacturer_docs_needed: boolean                       │
│   - historical_analysis_needed: boolean                     │
│   - problem_category: string                                │
│   - complexity_score: float                                 │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PARALLEL EXECUTION (3 branches)                             │
│                                                             │
│ ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│ │ Worker Agent 1  │  │ Worker Agent 2  │  │ Worker Agent│  │
│ │ SDCS Retrieval  │  │ Manufacturer    │  │ Case History│  │
│ │                 │  │ Documentation   │  │ Analysis    │  │
│ │ Output:         │  │                 │  │             │  │
│ │ - schematics[]  │  │ Output:         │  │ Output:     │  │
│ │ - equipment_list│  │ - guides[]      │  │ - similar[] │  │
│ │ - network_topo  │  │ - firmware_info │  │ - patterns  │  │
│ └─────────────────┘  └─────────────────┘  └──────────────┘ │
│         │                    │                    │         │
│         └────────────────────┴────────────────────┘         │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ Flow Action: Aggregate_Worker_Results                       │
│ - Collect all worker agent outputs                          │
│ - Handle partial failures gracefully                        │
│ - Create aggregated_context object                          │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Agent: AVISPL_Troubleshooting_Communicator_Agent            │
│ Input: aggregated_context                                   │
│ Output: troubleshooting_plan (structured)                   │
│   - steps[] (numbered, with expected outcomes)              │
│   - visual_docs[] (diagram links)                           │
│   - decision_criteria                                       │
│   - estimated_time                                          │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Now Assist Panel: Display_To_TSE                            │
│ - Render troubleshooting plan                               │
│ - Buttons: [Start Troubleshooting] [Not Helpful] [Report]  │
│ - Capture user interaction                                  │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Human Action: TSE Reviews and Executes Plan                │
│ - TSE works through troubleshooting steps                   │
│ - Outcome: Remote Success / Remote Failure / Escalated     │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Flow Action: Capture_Outcome_and_Feedback                   │
│ - Record resolution outcome                                 │
│ - Update case notes with executed steps                     │
│ - Collect feedback rating (1-5)                             │
│ - Feed data to learning pipeline                            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ END: Update Case Record                                     │
│ - Add AI_ASSISTED tag                                       │
│ - Log workflow execution time                               │
└─────────────────────────────────────────────────────────────┘
```

**Flow Configuration:**
```json
{
  "name": "Remote_Troubleshooting_Agentic_Workflow",
  "table": "sn_customerservice_case",
  "trigger_conditions": {
    "assignment_group": "TSE_Queue",
    "category": "Technical Support",
    "state": "assigned"
  },
  "manual_trigger": {
    "ui_action": "Get AI Troubleshooting Plan",
    "button_location": "case_form_header"
  },
  "timeout_minutes": 15,
  "error_handling": "graceful_degradation",
  "logging_level": "detailed",
  "cost_tracking": true
}
```

---

### 2.2 Knowledge Generation Agentic Workflow

```
Workflow: Knowledge_Generation_Agentic_Workflow
Sys ID: workflow_knowledge_generation
Table: sn_customerservice_case
Trigger: Case state changes to "Resolved" or "Closed"

┌─────────────────────────────────────────────────────────────┐
│ START: Case Resolved/Closed                                │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Flow Action: Case_Eligibility_Check                         │
│ - Resolution notes length >= 50 words                       │
│ - Case type = Technical (not administrative)                │
│ - Exclude Symphony auto-closures                            │
│ Output: eligible (true/false)                               │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼ [eligible = true]
┌─────────────────────────────────────────────────────────────┐
│ Agent: AVISPL_Knowledge_Evaluation_Orchestrator_Agent       │
│ Input: case_sys_id, resolution_notes, problem_description   │
│ Output: worthiness_score (high/medium/low)                  │
│   - completeness_score: float                               │
│   - reusability_score: float                                │
│   - duplication_check: boolean                              │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼ [high]     ▼ [medium]   ▼ [low]
   ┌────────┐   ┌────────┐   ┌────────┐
   │Generate│   │ Prompt │   │  Skip  │
   │  Auto  │   │  User  │   │   KB   │
   └───┬────┘   └───┬────┘   └───┬────┘
       │            │            │
       │            ▼            │
       │    ┌──────────────┐    │
       │    │ User Opts In?│    │
       │    └──┬───────┬───┘    │
       │       │ yes   │ no     │
       │       ▼       └────────┤
       │                        │
       └──────┬─────────────────┘
              │ [proceed with generation]
              ▼
┌─────────────────────────────────────────────────────────────┐
│ Agent: AVISPL_Knowledge_Content_Worker_Agent                │
│ Input: case_data, resolution_notes                          │
│ Output: draft_article (structured)                          │
│   - title                                                   │
│   - problem_statement                                       │
│   - symptoms[]                                              │
│   - equipment_affected                                      │
│   - root_cause                                              │
│   - resolution_steps[]                                      │
│   - verification_steps                                      │
│   - metadata (category, tags)                               │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ Agent: AVISPL_Knowledge_Review_Communicator_Agent           │
│ - Send notification to resolver                             │
│ - Display draft in Now Assist Panel                         │
│ - Present options: [Approve] [Edit] [Reject] [Defer]       │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬────────────┐
        │            │            │            │
        ▼ [approve]  ▼ [edit]     ▼ [reject]   ▼ [defer]
   ┌────────┐   ┌────────┐   ┌────────┐   ┌────────┐
   │Submit  │   │Capture │   │  Log   │   │Send    │
   │to KB   │   │Changes │   │Reason  │   │Reminder│
   │Workflow│   │then    │   │Update  │   │24hrs   │
   │        │   │Submit  │   │Model   │   │        │
   └───┬────┘   └───┬────┘   └───┬────┘   └───┬────┘
       │            │            │            │
       └────────────┴────────────┴────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ END: Feedback Loop Update                                   │
│ - Track approval/rejection patterns                         │
│ - Analyze common edits                                      │
│ - Refine agent instructions                                 │
└─────────────────────────────────────────────────────────────┘
```

**Flow Configuration:**
```json
{
  "name": "Knowledge_Generation_Agentic_Workflow",
  "table": "sn_customerservice_case",
  "trigger_conditions": {
    "state": ["resolved", "closed"],
    "category": "Technical Support",
    "resolution_notes": "not_empty"
  },
  "execution_priority": "low",
  "async_processing": true,
  "sla_exempt": true,
  "target_generation_rate": 0.80
}
```

---

## 3. Integration Hub Connections

### 3.1 SharePoint SDCS External Content Connector

```json
{
  "name": "SharePoint_SDCS_Connector",
  "type": "External Content Source",
  "sys_id": "ext_content_sharepoint_sdcs",
  "connection_type": "Microsoft SharePoint Online",
  "authentication": {
    "method": "OAuth 2.0",
    "credential_alias": "avispl_sharepoint_oauth",
    "scopes": ["Sites.Read.All", "Files.Read.All"]
  },
  "configuration": {
    "site_url": "https://avispl.sharepoint.com/sites/SDCS",
    "document_library": "Site Documentation",
    "folder_scope": "/folder_95_schematics",
    "crawl_schedule": "daily_midnight",
    "file_types": [".dwg", ".pdf", ".xlsx", ".docx"],
    "max_file_size_mb": 50
  },
  "indexing": {
    "enabled": true,
    "metadata_extraction": true,
    "ocr_enabled": false,
    "embedding_model": "text-embedding-3-large"
  },
  "security": {
    "folder_level_permissions": true,
    "pii_scanning": true,
    "data_masking": true
  },
  "performance": {
    "cache_ttl_hours": 24,
    "rate_limit_requests_per_minute": 100
  }
}
```

**Integration Hub Spoke:**
- **Spoke**: Microsoft SharePoint Online
- **Actions Used**:
  - `Search Documents`
  - `Get Document Metadata`
  - `Download Document`
  - `List Folder Contents`

---

### 3.2 Manufacturer Documentation Connectors

#### Extron Website Connector

```json
{
  "name": "Extron_Website_Connector",
  "type": "External Content Source",
  "sys_id": "ext_content_extron",
  "connection_type": "Web Crawler",
  "configuration": {
    "base_urls": [
      "https://www.extron.com/product/",
      "https://www.extron.com/downloads/",
      "https://www.extron.com/support/"
    ],
    "crawl_depth": 3,
    "crawl_schedule": "weekly_sunday",
    "respect_robots_txt": true,
    "file_types": [".pdf", ".html"],
    "content_selectors": {
      "troubleshooting_guides": ".support-document",
      "product_specs": ".spec-sheet",
      "firmware_downloads": ".firmware-link"
    }
  },
  "indexing": {
    "enabled": true,
    "deduplicate": true,
    "embedding_model": "text-embedding-3-large"
  },
  "performance": {
    "cache_ttl_hours": 168,
    "rate_limit_requests_per_minute": 30
  }
}
```

#### Polycom Support Connector

```json
{
  "name": "Polycom_Support_Connector",
  "type": "External Content Source",
  "sys_id": "ext_content_polycom",
  "connection_type": "Web Crawler",
  "configuration": {
    "base_urls": [
      "https://support.polycom.com/",
      "https://documents.polycom.com/"
    ],
    "crawl_depth": 3,
    "crawl_schedule": "weekly_sunday",
    "file_types": [".pdf", ".html"],
    "content_patterns": [
      "troubleshooting",
      "administrator guide",
      "quick start"
    ]
  },
  "indexing": {
    "enabled": true,
    "embedding_model": "text-embedding-3-large"
  }
}
```

---

### 3.3 Contract Management System Integration

```json
{
  "name": "Contract_Management_System_Integration",
  "type": "REST API Connection",
  "sys_id": "integration_contract_mgmt",
  "connection_details": {
    "base_url": "https://avispl-contracts.example.com/api/v2",
    "authentication": {
      "method": "API Key",
      "credential_alias": "contract_system_api_key"
    },
    "headers": {
      "Content-Type": "application/json",
      "Accept": "application/json"
    }
  },
  "endpoints": {
    "search_contracts": {
      "method": "POST",
      "path": "/contracts/search",
      "parameters": ["customer_name", "account_number", "email_domain"],
      "response_mapping": {
        "contract_id": "id",
        "contract_status": "status",
        "service_tier": "tier",
        "expiration_date": "expires_at",
        "equipment_covered": "equipment_list"
      }
    },
    "get_contract_details": {
      "method": "GET",
      "path": "/contracts/{contract_id}",
      "response_mapping": {
        "sla_terms": "service_level_agreement",
        "on_site_included": "includes_onsite_service",
        "support_hours": "coverage_hours"
      }
    }
  },
  "error_handling": {
    "retry_count": 3,
    "timeout_seconds": 30,
    "fallback_action": "flag_for_manual_lookup"
  }
}
```

---

## 4. Data Model Extensions

### 4.1 Case Table Extensions

**Table:** `sn_customerservice_case`

```json
{
  "custom_fields": [
    {
      "name": "u_ai_troubleshooting_plan_generated",
      "type": "boolean",
      "label": "AI Troubleshooting Plan Generated",
      "default_value": false
    },
    {
      "name": "u_ai_plan_helpful",
      "type": "choice",
      "label": "AI Plan Helpful",
      "choices": ["yes", "no", "not_used"],
      "default_value": "not_used"
    },
    {
      "name": "u_troubleshooting_plan_json",
      "type": "json",
      "label": "Troubleshooting Plan Data",
      "max_length": 10000
    },
    {
      "name": "u_remote_resolution_predicted",
      "type": "boolean",
      "label": "Remote Resolution Predicted"
    },
    {
      "name": "u_remote_resolution_actual",
      "type": "boolean",
      "label": "Remote Resolution Actual"
    },
    {
      "name": "u_kb_article_generated",
      "type": "boolean",
      "label": "KB Article Auto-Generated"
    },
    {
      "name": "u_kb_article_status",
      "type": "choice",
      "label": "KB Article Status",
      "choices": ["not_generated", "pending_review", "approved", "published", "rejected"]
    },
    {
      "name": "u_ai_enrichment_completed",
      "type": "boolean",
      "label": "AI Enrichment Completed"
    },
    {
      "name": "u_contract_validation_status",
      "type": "choice",
      "label": "Contract Validation",
      "choices": ["active", "expired", "not_found", "pending_verification"]
    }
  ]
}
```

---

### 4.2 Work Order Table Extensions

**Table:** `wm_order`

```json
{
  "custom_fields": [
    {
      "name": "u_ai_dispatch_recommendation",
      "type": "reference",
      "label": "AI Recommended Technician",
      "reference": "sys_user"
    },
    {
      "name": "u_skills_match_score",
      "type": "decimal",
      "label": "Skills Match Score",
      "scale": 2
    },
    {
      "name": "u_travel_time_minutes",
      "type": "integer",
      "label": "Estimated Travel Time (min)"
    },
    {
      "name": "u_work_order_briefing_json",
      "type": "json",
      "label": "AI Work Order Briefing",
      "max_length": 15000
    },
    {
      "name": "u_briefing_reviewed_by_tech",
      "type": "boolean",
      "label": "Briefing Reviewed by Technician"
    },
    {
      "name": "u_briefing_helpful_rating",
      "type": "integer",
      "label": "Briefing Helpfulness (1-5)"
    },
    {
      "name": "u_first_visit_resolution_predicted",
      "type": "boolean",
      "label": "First Visit Resolution Predicted"
    }
  ]
}
```

---

### 4.3 AI Agent Execution Log Table (Custom)

**Table:** `x_avispl_ai_agents_execution_log`

```json
{
  "label": "AI Agent Execution Log",
  "extends": "sys_metadata",
  "fields": [
    {
      "name": "agent_name",
      "type": "string",
      "label": "Agent Name",
      "mandatory": true
    },
    {
      "name": "workflow_name",
      "type": "string",
      "label": "Workflow Name"
    },
    {
      "name": "case_number",
      "type": "reference",
      "label": "Related Case",
      "reference": "sn_customerservice_case"
    },
    {
      "name": "execution_start_time",
      "type": "glide_date_time",
      "label": "Execution Start"
    },
    {
      "name": "execution_end_time",
      "type": "glide_date_time",
      "label": "Execution End"
    },
    {
      "name": "duration_seconds",
      "type": "decimal",
      "label": "Duration (seconds)"
    },
    {
      "name": "status",
      "type": "choice",
      "label": "Status",
      "choices": ["success", "partial_success", "failure", "timeout"]
    },
    {
      "name": "input_parameters",
      "type": "json",
      "label": "Input Parameters"
    },
    {
      "name": "output_data",
      "type": "json",
      "label": "Output Data"
    },
    {
      "name": "token_usage",
      "type": "integer",
      "label": "Tokens Used"
    },
    {
      "name": "estimated_cost_usd",
      "type": "decimal",
      "label": "Estimated Cost (USD)",
      "scale": 4
    },
    {
      "name": "error_message",
      "type": "string",
      "label": "Error Message",
      "max_length": 4000
    },
    {
      "name": "user_feedback_rating",
      "type": "integer",
      "label": "User Feedback (1-5)"
    },
    {
      "name": "user_feedback_comments",
      "type": "string",
      "label": "User Comments",
      "max_length": 1000
    }
  ],
  "indexes": [
    "agent_name",
    "workflow_name",
    "case_number",
    "execution_start_time"
  ]
}
```

---

## 5. Retriever Configurations

### 5.1 ServiceNow Case History Retriever

```json
{
  "name": "ServiceNow_Case_History_Retriever",
  "sys_id": "retriever_case_history",
  "type": "Table Retriever",
  "description": "Searches historical closed cases for resolution patterns",
  "configuration": {
    "table": "sn_customerservice_case",
    "search_fields": [
      "short_description",
      "description",
      "resolution_notes",
      "close_notes",
      "work_notes"
    ],
    "filter_conditions": "state=resolved^ORstate=closed^closed_atRELATIVEGT@dayofweek@ago@730",
    "result_fields": [
      "number",
      "short_description",
      "resolution_notes",
      "close_notes",
      "closed_at",
      "u_equipment_model",
      "location"
    ],
    "max_results": 15,
    "min_relevance_score": 0.65,
    "search_method": "hybrid",
    "embedding_model": "text-embedding-3-large",
    "keyword_boost": 1.2
  },
  "context_window": {
    "include_related_records": true,
    "related_tables": ["incident", "wm_order"],
    "max_context_tokens": 8000
  }
}
```

---

### 5.2 SDCS SharePoint Retriever

```json
{
  "name": "SDCS_SharePoint_Retriever",
  "sys_id": "retriever_sdcs_sharepoint",
  "type": "External Content Retriever",
  "description": "Retrieves site-specific schematics and documentation from SharePoint SDCS",
  "configuration": {
    "external_content_source": "ext_content_sharepoint_sdcs",
    "search_fields": ["file_name", "file_content", "metadata"],
    "folder_filters": ["/folder_95_schematics"],
    "file_type_filters": [".dwg", ".pdf", ".xlsx"],
    "max_results": 10,
    "min_relevance_score": 0.75,
    "search_method": "semantic",
    "embedding_model": "text-embedding-3-large"
  },
  "metadata_boost": {
    "customer_name": 1.5,
    "site_location": 1.5,
    "equipment_model": 1.3,
    "file_type": 1.1
  },
  "result_enrichment": {
    "include_download_link": true,
    "include_preview": true,
    "extract_equipment_list": true
  }
}
```

---

### 5.3 Equipment Technical Specs Retriever

```json
{
  "name": "Equipment_Technical_Specs_Retriever",
  "sys_id": "retriever_equipment_specs",
  "type": "Multi-Source External Content Retriever",
  "description": "Searches manufacturer documentation for equipment specifications",
  "configuration": {
    "external_content_sources": [
      "ext_content_extron",
      "ext_content_polycom"
    ],
    "search_fields": ["title", "content", "product_code"],
    "content_type_filters": ["specification_sheet", "user_manual", "troubleshooting_guide"],
    "max_results_per_source": 5,
    "min_relevance_score": 0.70,
    "search_method": "semantic",
    "embedding_model": "text-embedding-3-large"
  },
  "result_ranking": {
    "prioritize_official_docs": true,
    "boost_recent_documents": true,
    "recency_decay_days": 365
  }
}
```

---

## 6. Now Assist Panel Components

### 6.1 Troubleshooting Plan Display Panel

```json
{
  "name": "now_assist_troubleshooting_panel",
  "sys_id": "panel_troubleshooting_display",
  "type": "Now Assist Panel",
  "context": "Case Form",
  "location": "Right Panel",
  "configuration": {
    "title": "AI Troubleshooting Plan",
    "icon": "brain-circuit",
    "collapsible": true,
    "default_state": "expanded",
    "refresh_on_update": true
  },
  "sections": [
    {
      "section_id": "equipment_context",
      "title": "Equipment Context",
      "type": "info_card",
      "fields": ["equipment_model", "location", "network_topology_link"]
    },
    {
      "section_id": "troubleshooting_steps",
      "title": "Troubleshooting Steps",
      "type": "checklist",
      "collapsible_items": true,
      "fields_per_step": [
        "step_number",
        "action_description",
        "expected_outcome",
        "reference_link",
        "estimated_time"
      ]
    },
    {
      "section_id": "decision_point",
      "title": "Decision Point",
      "type": "decision_card",
      "options": ["resolved", "escalate_to_field"]
    },
    {
      "section_id": "additional_resources",
      "title": "Additional Resources",
      "type": "link_list",
      "fields": ["sdcs_schematic", "manufacturer_guide", "past_case_reference"]
    }
  ],
  "actions": [
    {
      "button_label": "Start Troubleshooting",
      "action_type": "client_script",
      "script_name": "startTroubleshootingTimer"
    },
    {
      "button_label": "Not Helpful",
      "action_type": "feedback_collection",
      "feedback_fields": ["reason", "missing_information"]
    },
    {
      "button_label": "Report Issue",
      "action_type": "create_incident",
      "assignment_group": "AI_Support_Team"
    }
  ]
}
```

---

### 6.2 Knowledge Article Review Panel

```json
{
  "name": "now_assist_kb_review_panel",
  "sys_id": "panel_kb_article_review",
  "type": "Now Assist Panel",
  "context": "Case Form",
  "trigger": "Case State = Resolved/Closed AND KB Article Generated",
  "configuration": {
    "title": "Review AI-Generated Knowledge Article",
    "icon": "document-check",
    "notification_type": "modal",
    "dismissible": true
  },
  "sections": [
    {
      "section_id": "article_preview",
      "title": "Article Preview",
      "type": "rich_text_display",
      "editable": true,
      "fields": [
        "article_title",
        "problem_statement",
        "symptoms",
        "equipment_affected",
        "root_cause",
        "resolution_steps",
        "verification"
      ]
    },
    {
      "section_id": "article_metadata",
      "title": "Metadata",
      "type": "info_card",
      "fields": ["category", "tags", "target_audience"]
    }
  ],
  "actions": [
    {
      "button_label": "Approve & Publish",
      "button_style": "primary",
      "action_type": "flow_trigger",
      "flow_name": "Submit_To_Knowledge_Workflow",
      "parameters": {"approval_status": "approved"}
    },
    {
      "button_label": "Edit & Approve",
      "button_style": "secondary",
      "action_type": "inline_edit_mode",
      "capture_changes": true
    },
    {
      "button_label": "Reject",
      "button_style": "tertiary",
      "action_type": "feedback_collection",
      "feedback_fields": ["rejection_reason"]
    },
    {
      "button_label": "Review Later",
      "button_style": "tertiary",
      "action_type": "defer",
      "reminder_hours": 24
    }
  ]
}
```

---

### 6.3 Mobile Work Order Briefing Panel

```json
{
  "name": "now_assist_mobile_briefing",
  "sys_id": "panel_mobile_work_order_briefing",
  "type": "Now Assist Panel",
  "context": "Work Order Form",
  "platform": "Mobile",
  "configuration": {
    "title": "Work Order Briefing",
    "icon": "clipboard-list",
    "offline_mode": true,
    "sync_on_connect": true
  },
  "sections": [
    {
      "section_id": "quick_facts",
      "title": "Quick Facts",
      "type": "summary_card",
      "always_visible": true,
      "fields": [
        "site_name",
        "site_address_with_map",
        "equipment_model",
        "issue_summary",
        "priority",
        "estimated_time"
      ]
    },
    {
      "section_id": "problem_details",
      "title": "Problem Details",
      "type": "expandable_section",
      "collapsed_by_default": true,
      "content_type": "rich_text"
    },
    {
      "section_id": "already_tried",
      "title": "Already Tried",
      "type": "expandable_section",
      "collapsed_by_default": true,
      "content_type": "bullet_list"
    },
    {
      "section_id": "recommended_approach",
      "title": "Recommended Approach",
      "type": "expandable_section",
      "collapsed_by_default": false,
      "content_type": "checklist"
    },
    {
      "section_id": "documentation",
      "title": "Documentation",
      "type": "expandable_section",
      "collapsed_by_default": true,
      "content_type": "file_links",
      "offline_download": true
    }
  ],
  "actions": [
    {
      "button_label": "Download Offline Briefing",
      "icon": "download",
      "action_type": "pdf_download",
      "file_name": "work_order_{number}_briefing.pdf"
    },
    {
      "button_label": "Navigate to Site",
      "icon": "navigation",
      "action_type": "open_maps",
      "map_provider": "device_default"
    },
    {
      "button_label": "Contact TSE",
      "icon": "message",
      "action_type": "direct_message",
      "recipient_field": "escalated_by"
    },
    {
      "button_label": "Start Work Order",
      "icon": "play",
      "action_type": "update_state",
      "new_state": "work_in_progress",
      "start_timer": true
    }
  ]
}
```

---

## 7. Skills & AI Model Configurations

### 7.1 Classification Skills

#### Problem Category Classifier

```json
{
  "name": "Classification_Problem_Category",
  "sys_id": "skill_problem_classifier",
  "type": "Classification Skill",
  "model": "Claude 3.5 Sonnet",
  "categories": [
    {
      "name": "connectivity_issue",
      "description": "Network connectivity, cable issues, signal problems"
    },
    {
      "name": "hardware_failure",
      "description": "Physical equipment failure, component damage"
    },
    {
      "name": "configuration_error",
      "description": "Settings misconfiguration, programming errors"
    },
    {
      "name": "software_bug",
      "description": "Firmware bugs, software glitches"
    },
    {
      "name": "user_error",
      "description": "Incorrect operation, misunderstanding of functionality"
    }
  ],
  "confidence_threshold": 0.75,
  "multi_label": false,
  "few_shot_examples": 5
}
```

#### Knowledge Worthiness Classifier

```json
{
  "name": "Classification_Knowledge_Worthiness",
  "sys_id": "skill_knowledge_classifier",
  "type": "Classification Skill",
  "model": "Claude 3.5 Haiku",
  "categories": [
    {
      "name": "high",
      "description": "Clear problem, documented solution, high reusability",
      "threshold": 0.80
    },
    {
      "name": "medium",
      "description": "Moderate reusability, may need human refinement",
      "threshold": 0.50
    },
    {
      "name": "low",
      "description": "Generic solution, low reusability, insufficient detail",
      "threshold": 0.00
    }
  ],
  "evaluation_criteria": [
    "problem_clarity",
    "solution_completeness",
    "step_by_step_documentation",
    "applicability_scope",
    "uniqueness"
  ]
}
```

---

### 7.2 Generation Skills

#### Knowledge Article Generator

```json
{
  "name": "Generation_Knowledge_Article",
  "sys_id": "skill_kb_generation",
  "type": "Generation Skill",
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.5,
  "max_tokens": 4000,
  "template": {
    "name": "avispl_kb_article_template",
    "structure": {
      "title": "{{equipment_model}} - {{problem_summary}} Resolution",
      "sections": [
        "Problem Statement",
        "Symptoms",
        "Equipment Affected",
        "Root Cause",
        "Resolution Steps",
        "Verification",
        "Additional Notes"
      ]
    }
  },
  "formatting_rules": {
    "use_bullet_points": true,
    "active_voice": true,
    "tense": "present",
    "max_paragraph_sentences": 3,
    "include_model_numbers": true
  },
  "validation": {
    "min_resolution_steps": 2,
    "max_resolution_steps": 15,
    "required_fields": ["title", "problem_statement", "resolution_steps"]
  }
}
```

#### Step-by-Step Instructions Generator

```json
{
  "name": "Generation_Step_By_Step_Instructions",
  "sys_id": "skill_instruction_generation",
  "type": "Generation Skill",
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.4,
  "max_tokens": 3000,
  "output_format": {
    "structure": "numbered_list",
    "per_step_fields": [
      "step_number",
      "action_description",
      "expected_outcome",
      "estimated_time_minutes",
      "reference_source"
    ]
  },
  "prioritization_strategy": {
    "method": "success_rate_weighted",
    "fallback": "manufacturer_recommended_sequence",
    "complexity_order": "simple_to_complex"
  }
}
```

---

### 7.3 Summarization Skills

#### Technical Documentation Summarizer

```json
{
  "name": "Summarization_Technical_Documentation",
  "sys_id": "skill_tech_summarization",
  "type": "Summarization Skill",
  "model": "Claude 3.5 Sonnet",
  "temperature": 0.3,
  "max_tokens": 2000,
  "summarization_style": {
    "focus": "key_technical_points",
    "audience": "technical_support_engineers",
    "length": "concise",
    "preserve_specifics": ["model_numbers", "error_codes", "measurements"]
  },
  "output_format": {
    "structure": "bullet_points",
    "max_bullets": 8,
    "include_source_references": true
  }
}
```

#### Mobile-Optimized Summarizer

```json
{
  "name": "Summarization_Mobile_Optimized",
  "sys_id": "skill_mobile_summary",
  "type": "Summarization Skill",
  "model": "Claude 3.5 Haiku",
  "temperature": 0.3,
  "max_tokens": 1000,
  "mobile_optimization": {
    "max_sentence_length": 20,
    "visual_formatting": true,
    "scannable_structure": true,
    "emoji_icons": false
  },
  "output_sections": {
    "quick_facts": "3-5 key points",
    "action_items": "prioritized list",
    "context": "2-3 sentences"
  }
}
```

---

## 8. Security & Access Controls

### 8.1 Role Definitions

```json
{
  "roles": [
    {
      "name": "x_avispl_ai_agents.user",
      "label": "AVISPL AI Agents User",
      "description": "Basic access to view AI agent outputs and provide feedback",
      "assigned_to": ["TSE", "TSR", "Field Technician", "Case Manager"]
    },
    {
      "name": "x_avispl_ai_agents.admin",
      "label": "AVISPL AI Agents Administrator",
      "description": "Full administrative access to configure agents and workflows",
      "assigned_to": ["AI Platform Administrator", "ServiceNow Admin"]
    },
    {
      "name": "x_avispl_ai_agents.analyst",
      "label": "AVISPL AI Agents Analyst",
      "description": "Access to performance analytics and execution logs",
      "assigned_to": ["Process Improvement Team", "Management"]
    }
  ]
}
```

---

### 8.2 Access Control Lists (ACLs)

#### Agent Execution ACL

```json
{
  "name": "x_avispl_ai_agents.agent_execute",
  "type": "ACL",
  "object": "AI Agent Workflow",
  "operation": "execute",
  "conditions": {
    "roles": ["x_avispl_ai_agents.user", "x_avispl_ai_agents.admin"],
    "additional_conditions": "user.active=true AND user.department IN ['Support','Field Service']"
  }
}
```

#### SDCS Data Access ACL

```json
{
  "name": "x_avispl_ai_agents.sdcs_access",
  "type": "ACL",
  "object": "External Content Source - SDCS",
  "operation": "read",
  "conditions": {
    "roles": ["x_avispl_ai_agents.user", "x_avispl_ai_agents.admin"],
    "folder_restrictions": "/folder_95_schematics",
    "data_classification": "internal_use_only"
  },
  "security_controls": {
    "pii_masking": true,
    "audit_logging": true,
    "download_restrictions": false
  }
}
```

---

### 8.3 Now Assist Guardian Configuration

```json
{
  "name": "AVISPL_AI_Agents_Guardian_Policy",
  "sys_id": "guardian_policy_avispl",
  "content_filtering": {
    "enabled": true,
    "block_categories": [
      "hate_speech",
      "violence",
      "sexual_content",
      "self_harm"
    ],
    "warn_categories": [
      "medical_advice",
      "financial_advice",
      "legal_advice"
    ]
  },
  "pii_protection": {
    "enabled": true,
    "detect": ["ssn", "credit_card", "email", "phone", "address"],
    "action": "mask",
    "logging": true
  },
  "output_validation": {
    "enabled": true,
    "max_response_length": 10000,
    "require_source_citations": true,
    "block_hallucinations": {
      "enabled": true,
      "confidence_threshold": 0.70
    }
  },
  "rate_limiting": {
    "enabled": true,
    "per_user_per_hour": 50,
    "per_workflow_per_day": 1000
  }
}
```

---

### 8.4 Sensitive Data Handler Rules

```json
{
  "sensitive_data_rules": [
    {
      "name": "Customer_PII_Protection",
      "data_types": ["email", "phone_number", "address"],
      "tables": ["sn_customerservice_case", "customer_contact"],
      "action": "mask",
      "mask_format": "partial",
      "apply_to_agents": "all"
    },
    {
      "name": "Contract_Financial_Data_Protection",
      "data_types": ["pricing", "discount_percentage", "payment_terms"],
      "tables": ["contract"],
      "action": "redact",
      "apply_to_agents": ["SDCS_Retrieval", "Case_Enrichment"]
    },
    {
      "name": "SharePoint_Credentials_Protection",
      "data_types": ["password", "access_key", "api_token"],
      "source": "sharepoint_sdcs_connector",
      "action": "block",
      "apply_to_agents": "all"
    }
  ]
}
```

---

## Deployment Checklist

### Phase 1: Environment Setup (Week 1-2)

- [ ] Provision scoped application: `x_avispl_ai_agents`
- [ ] Configure OAuth for SharePoint SDCS connector
- [ ] Create custom tables and extend existing tables
- [ ] Define roles and ACLs
- [ ] Configure Now Assist Guardian policies
- [ ] Set up audit logging for AI agent executions

### Phase 2: Agent Configuration (Week 2-4)

- [ ] Create all 15 agent configurations
- [ ] Configure agent instructions and tool assignments
- [ ] Test individual agents in isolated mode
- [ ] Configure retrievers for all data sources
- [ ] Index SharePoint SDCS content
- [ ] Index manufacturer websites (Extron, Polycom)

### Phase 3: Workflow Development (Week 3-6)

- [ ] Build Remote Troubleshooting Agentic Workflow
- [ ] Build Knowledge Generation Agentic Workflow
- [ ] Build Field Dispatch Agentic Workflow
- [ ] Build Case Queue Intelligence Workflow
- [ ] Configure Now Assist Panel components
- [ ] Implement error handling and fallback logic

### Phase 4: Integration & Testing (Week 7-10)

- [ ] Configure Integration Hub connections
- [ ] Test SDCS SharePoint retrieval
- [ ] Test manufacturer documentation retrieval
- [ ] Test contract management system integration
- [ ] Validate AWA integration for queue assignment
- [ ] Performance testing (latency, token usage)
- [ ] Security testing (PII masking, access controls)

### Phase 5: User Acceptance Testing (Week 13-14)

- [ ] Pilot with 5 TSEs for troubleshooting agent
- [ ] Pilot with 3 field technicians for dispatch agent
- [ ] Test knowledge article generation with 10 resolved cases
- [ ] Collect user feedback via surveys
- [ ] Refine agent instructions based on feedback
- [ ] Optimize retriever relevance tuning

### Phase 6: Production Deployment (Week 15-16)

- [ ] Deploy to production instance
- [ ] Enable workflows for all eligible cases
- [ ] Monitor execution logs and error rates
- [ ] Track success metrics dashboards
- [ ] Conduct training sessions for all user personas
- [ ] Establish feedback collection mechanisms

---

## Monitoring & Analytics

### Key Performance Dashboards

**Dashboard 1: Agent Execution Metrics**
- Total agent executions per day
- Average execution time by agent
- Success rate by workflow
- Token usage and cost trends

**Dashboard 2: Business Outcomes**
- Remote resolution rate trend
- Case triage time reduction
- Knowledge article generation rate
- First-visit resolution rate improvement

**Dashboard 3: User Adoption**
- Agent usage by persona (TSE, field tech, case manager)
- User feedback ratings distribution
- Most/least used workflows
- Feature adoption over time

---

**Document Version:** 1.0
**Last Updated:** December 5, 2025
**Next Review:** January 5, 2026

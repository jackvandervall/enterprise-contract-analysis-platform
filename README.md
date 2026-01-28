# Enterprise Contract Analysis Agent (Case Study)

> **Note:** This repository serves as a technical showcase for a proprietary application. Due to NDA and IP restrictions, the source code is not public.

![Status](https://img.shields.io/badge/Status-Production-success)
![Stack](https://img.shields.io/badge/Stack-React_|_Supabase_|_n8n-blue)
![Focus](https://img.shields.io/badge/Focus-AI_Agents_&_Compliance-purple)

## Description

Showcasing a specialized, internal AI system designed to automate the analysis and comparison of complex business documents (quotes, contracts, NDAs). Acting like a domain expert, this platform will validate incoming documents against:
1.  **Industry Standard Conditions** (Sector-specific legal frameworks).
2.  **Internal Compliance Checklists** (Client-specific business rules).
3.  **Commercial Risk Logic** (Price validity, liability caps, etc.).

![Dashboard Preview](assets/kpi-dashboard-preview.jpg)

## Real-World Impact

During the first month of deployment, the system demonstrated immediate value:

* **Concrete Discrepancies:** Identified **29 specific mismatches** between Purchase Orders (POs) and Sales Contracts.
* **Critical Risk Mitigation:** Flagged **7 critical and high-impact risks** related to liability clauses, compliance gaps, and conflicting Terms & Conditions.
* **Operational Protection:** Directly prevented financial and operational exposure by proactively detecting subtle deviations in delivery schedules, payment terms, and scope creep.

## Architecture & Agentic Workflow

The system utilizes a multi-agent architecture where a central orchestrator routes user requests to specialized agents:

1.  **PDF Tool:** Handles OCR, text extraction, and general document comparison.
2.  **Compliance Validator:** Specifically checks documents against strict industry terms.
3.  **Risk Assessor (KPI Agent):** Structures the output into risk categories and assigns a **Severity Score** (Low to Crucial).

## Key Features

-   **Context-Rich Analysis**: The LLM is injected with specific business context, preventing generic hallucinations.
-   **Severity Matching Algorithm**: Distinguishes between trivial text differences (e.g., phrasing) and critical contractual risks (e.g., liability terms).
-   **Multi-Agent Orchestration**: Powered by n8n, allowing for complex, branching logic flows that single-prompt LLMs cannot handle.
-   **Secure Authentication**: Role-based access control (RBAC) via Supabase Auth with manual admin approval flows.
-   **Real-time Dashboard**: Visualizes risk distribution and historical analysis using Recharts.

## Technologies Used

React, TypeScript, Vite, Tailwind CSS, shadcn/ui, Supabase, PostgreSQL, n8n, Anthropic Claude, Google Gemini.

## Credits
Developed by Jack van der Vall in collaboration with a Dutch industrial piping and prefabrication contractor specializing in large-scale energy and utility infrastructure.

---

*Copyright © 2025. All rights reserved.*

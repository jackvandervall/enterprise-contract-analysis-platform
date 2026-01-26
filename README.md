# Enterprise Contract Analysis Agent (Case Study)

> **Note:** This repository serves as a technical showcase for a proprietary application developed for a mid-sized enterprise client in the manufacturing sector. Due to NDA and IP restrictions, the source code is not public.

![Status](https://img.shields.io/badge/Status-Production-success)
![Stack](https://img.shields.io/badge/Stack-React_|_Supabase_|_n8n-blue)
![Focus](https://img.shields.io/badge/Focus-AI_Agents_&_Compliance-purple)

## 📖 Overview

The is a specialized, internal AI system designed to automate the analysis and comparison of complex business documents (quotes, contracts, NDAs).

Unlike generic "Copilot" tools which only summarize text, this platform acts as a Domain Expert and validates incoming documents against:
1.  **Industry Standard Conditions** (Sector-specific legal frameworks).
2.  **Internal Compliance Checklists** (Client-specific business rules).
3.  **Commercial Risk Logic** (Price validity, liability caps, etc.).

## 📈 Real-World Impact

![Dashboard Preview](assets/kpi-dashboard-preview.jpg)
*Figure 1: Preview showcasing Key Performance Indicator dashboard.*

During the first month of deployment, the system demonstrated immediate value:

* **Concrete Discrepancies:** Identified **29 specific mismatches** between Purchase Orders (POs) and Sales Contracts.
* **Critical Risk Mitigation:** Flagged **7 critical and high-impact risks** related to liability clauses, compliance gaps, and conflicting Terms & Conditions (T&Cs).
* **Operational Protection:** Directly prevented financial and operational exposure by proactively detecting subtle deviations in delivery schedules, payment terms, and scope creep.

## 🏗 Architecture & Agentic Workflow

The system utilizes a multi-agent architecture where a central orchestrator routes user requests to specialized agents:

1.  **PDF Tool:** Handles OCR, text extraction, and general document comparison.
2.  **Compliance Validator:** Specifically checks documents against strict industry terms.
3.  **Risk Assessor (KPI Agent):** Structures the output into risk categories and assigns a **Severity Score** (Low to Crucial).

## ✨ Key Technical Features

-   **Context-Rich Analysis**: The LLM is injected with specific business context, preventing generic hallucinations.
-   **Severity Matching Algorithm**: Distinguishes between trivial text differences (e.g., phrasing) and critical contractual risks (e.g., liability terms).
-   **Multi-Agent Orchestration**: Powered by n8n, allowing for complex, branching logic flows that single-prompt LLMs cannot handle.
-   **Secure Authentication**: Role-based access control (RBAC) via Supabase Auth with manual admin approval flows.
-   **Real-time Dashboard**: Visualizes risk distribution and historical analysis using Recharts.

## 🛠 Tech Stack

| Component | Technology | Reason for Choice |
| :--- | :--- | :--- |
| **Frontend** | React 18, TypeScript, Vite | Type safety and performance. |
| **Styling** | Tailwind CSS, shadcn/ui | Rapid UI development and accessibility. |
| **Backend** | Supabase (PostgreSQL) | Built-in Auth and Row Level Security (RLS). |
| **Orchestration** | n8n (Self-hosted) | Low-code backend logic for AI chains. |
| **LLM Models** | Anthropic Claude 3.5 | Superior reasoning for complex legal texts. |

## ⚙️ How It Works (Under the Hood)

### 1. The Data Layer (Supabase)
The application relies on a strictly typed PostgreSQL schema.
* **Documents Table:** Stores metadata and vector embeddings (if applicable).
* **Analysis Table:** JSONB columns store the structured output from the AI agents.
* **RLS Policies:** Ensures users can only access documents within their authorized department.

### 2. The AI Orchestration (n8n)
Instead of a simple API call, the backend triggers a complex workflow:
1.  **Webhook Trigger:** Receives the prompt + PDF buffer.
2.  **Router Node:** Classifies intent (e.g., "Is this a comparison?" vs "Is this a checklist check?").
3.  **LLM Processing:**
    * *Branch A:* Uses Claude 4 Sonnet for deep reasoning tasks.
    * *Branch B:* Uses Gemini 2.5 Flash for simple data extraction (cost optimization).
4.  **JSON Formatting:** The final output is forced into a strict JSON schema for the frontend to render.

### 3. Compliance & Privacy Strategy
Since this tool handles sensitive legal data, a "Privacy-First" strategy was implemented:
* **Data Sovereignty:** All data is hosted within EU regions (Frankfurt).
* **Zero-Training Policy:** We exclusively use Enterprise/Paid API tiers which contractually agree not to train models on submitted data.
* **Model Filtering:** By careful examination of privacy policies, high-risk models (e.g., non-GDPR-compliant or non-transparent data policies) have been avoided.

## 🚀 Development Workflow

*This section illustrates the environment setup used during development.*

### Prerequisites
-   Node.js 18+
-   Supabase CLI
-   n8n Instance

### Environment Configuration
The application requires tight integration between the frontend and the AI orchestration layer.

```bash
# Example .env configuration
VITE_SUPABASE_URL=[https://xyz.supabase.co](https://xyz.supabase.co)
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1...
VITE_N8N_WEBHOOK_URL=[https://ai.internal-platform.com/webhook/process](https://ai.internal-platform.com/webhook/process)
```

### Project Structure

```
src/
├── components/          # Shadcn UI components & Custom Risk Cards
├── pages/               # Dashboard, Chat Interface, Document Library
├── lib/                 # Supabase client & Utils
├── hooks/               # Custom React Query hooks for real-time data
└── types/               # Shared TypeScript interfaces (DB <-> Frontend)

```

---

*Copyright © 2025. All rights reserved.*

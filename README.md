Sentinel Agent Runtime

A governed AI execution runtime for regulated browser workflows

Sentinel Agent Runtime is an enterprise-grade managed AI browser agent platform that enables organizations to safely deploy AI agents inside the browser without sacrificing security, auditability, or policy control.

Unlike consumer AI extensions, Sentinel is designed for regulated environments (finance, compliance, internal ops), where every AI action must be explainable, enforceable, and auditable.

🚨 The Problem

Organizations want to use AI agents to automate browser-based workflows (e.g. invoice processing, internal portals, dashboards), but:

❌ AI browser agents can leak sensitive data

❌ No enforceable enterprise policies

❌ No audit trail or replayability

❌ No role-based or domain-based restrictions

As a result, security teams ban AI agents entirely, forcing employees back to manual work.

✅ The Solution

Sentinel Agent Runtime introduces a governed AI execution model:

AI agents can act inside the browser

But only within admin-defined policies

Every action is logged, validated, and auditable

Execution happens locally in the browser

Governance and reasoning happen server-side

Execution is sandboxed. Intelligence is controlled. Trust is enforced.

🎯 MVP Scope (Frozen)

This repository implements a focused MVP for a finance operations workflow:

Extract invoice totals and vendor names from a web-based invoice portal using a policy-aware AI agent.

What the MVP Includes

Chrome extension that executes agent steps in the browser

Backend agent orchestrator with policy enforcement

Structured AI planning (no free-form execution)

Immutable audit logging for every agent action

Admin-defined policy via configuration

Explicitly Out of Scope (by design)

Consumer AI chat UX

Multiple workflows

Policy UI (config-only for MVP)

Human approval mid-execution

Multi-tenant billing

LLM experimentation playground

This restraint is intentional and mirrors real enterprise systems.

🧠 Core Design Principles
1. Policy First

AI agents never reason or act outside policy boundaries.
Policies are enforced at:

Plan generation time

Step execution time

Data extraction time

2. Execution in the Browser

All DOM access and page interaction happen locally inside the browser extension to:

Preserve same-origin guarantees

Prevent raw data exfiltration

Reduce backend blast radius

3. Structured Agent Execution

Agents operate on explicit, typed steps, not free-form actions.

{
  "action": "EXTRACT_FIELD",
  "field": "invoice_total"
}

4. Auditability by Default

Every agent action emits an immutable audit event:

What happened

Why it happened

Whether it was allowed or blocked

🏗️ High-Level Architecture
Browser Extension (Execution Plane)
        │
        │ Secure RPC
        ▼
Agent Gateway (Auth & Rate Limiting)
        │
        ▼
Policy Engine (Enforcement)
        │
        ▼
Agent Orchestrator (Planning)
        │
        ▼
Audit Log Service (Append-only)


Key separation:

Execution Plane → Browser

Control Plane → Backend

🔐 Policy Model (MVP)

Policies are declarative and enforced at runtime.

allowed_domains:
  - invoices.example.com

allowed_actions:
  - READ_TABLE
  - EXTRACT_FIELD

allowed_fields:
  - vendor_name
  - invoice_total

max_steps: 10


If a policy is violated, execution is immediately terminated and logged.

📜 Audit Logging

Every agent interaction produces an append-only audit event.

{
  "timestamp": "2026-01-16T10:12:30Z",
  "actor": "agent",
  "action": "EXTRACT_FIELD",
  "field": "invoice_total",
  "status": "allowed",
  "page_hash": "abc123"
}


This enables:

Compliance audits

Post-incident analysis

Replayable execution (future work)

🧱 Repository Structure
sentinel-agent-runtime/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── agent-loop.md
│   ├── policy-model.md
│   └── threat-model.md
│
├── extension/
│   ├── manifest.json
│   ├── background/
│   ├── content/
│   ├── ui/
│   └── shared/
│
├── backend/
│   ├── cmd/
│   │   ├── gateway/
│   │   ├── orchestrator/
│   │   └── auditor/
│   ├── internal/
│   │   ├── agent/
│   │   ├── policy/
│   │   ├── audit/
│   │   └── auth/
│   └── pkg/
│
├── configs/
│   └── policy.yaml
│
├── scripts/
│   └── dev.sh
│
└── Makefile

🛠️ Tech Stack
Browser Extension

TypeScript

Chrome Extension Manifest V3

Content scripts + background service worker

Backend

Go (deterministic, infra-grade)

JSON-over-HTTPS / gRPC

PostgreSQL (metadata)

Object storage (audit logs)

AI

Single planner model

Strict JSON schema output

No chain-of-thought storage

🧪 Current Status

🚧 Active Development — MVP Phase

 Extension → backend communication

 Agent planning loop

 Policy enforcement

 Audit log persistence

🧠 Why This Project Exists

This project is intentionally designed to explore:

AI governance

Secure agent execution

Browser-based enforcement

Enterprise auditability

It reflects real-world constraints faced by companies deploying AI in regulated environments.



If you are reviewing this repo

Start with:

docs/architecture.md

docs/agent-loop.md

docs/threat-model.md
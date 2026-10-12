# Prompts Log — VitalSync Sprint 13

This file records the prompts used to prepare the planning artifacts. Update it with the actual prompts and tools used; do not claim that a prompt was used if it was not.

## Prompt 1 — Product requirements

> Act as a product manager for VitalSync, a healthcare appointment and patient-management dashboard. Create a planning-only PRD with problem statement, target users, goals, non-goals, user stories, P0/P1/P2 prioritization, functional requirements, non-functional requirements, edge cases, and acceptance criteria. Do not write application code. Avoid claiming medical or regulatory compliance.

**Purpose:** Establish scope and acceptance criteria before implementation.

## Prompt 2 — Responsive Figma review

> Review the VitalSync screens for sign-in, dashboard, appointments, appointment details, patient details, and My Appointments. Define desktop, tablet, and mobile behavior for each screen. Identify navigation changes, table-to-card transformations, overflow risks, touch-target concerns, and loading/empty/error states. Do not invent details that are not visible in the design; list assumptions separately.

**Purpose:** Plan responsive behavior and Figma handoff.

## Prompt 3 — Fullstack architecture

> Propose a planning-level architecture for VitalSync using React + TypeScript, Tailwind CSS, TanStack Query, Node.js/Express + TypeScript, and MongoDB/Mongoose. Include client/API/database boundaries, validation, authorization, error handling, and a Mermaid architecture diagram. Do not generate functional source code.

**Purpose:** Document system boundaries and technical choices.

## Prompt 4 — Frontend state model

> Design a frontend state tree for VitalSync. Separate server state from client UI state. Use TanStack Query for API-backed patients and appointments; use Redux Toolkit only for genuinely shared client state. Include auth state, filters, pagination, modal/sidebar state, cache invalidation after mutations, and loading/error behavior. Output a concise tree and rationale, not code.

**Purpose:** Avoid duplicate sources of truth and make state ownership explicit.

## Prompt 5 — REST API contracts

> Define REST API contracts for VitalSync under `/api/v1` for authentication, dashboard summary, appointments, and patients. For each endpoint include method, purpose, query/path parameters, example request and response, validation rules, authorization expectations, and error cases. Use fictional data only. Do not implement the API.

**Purpose:** Define the client/server contract before parallel implementation.

## Prompt 6 — MongoDB ERD

> Design a MongoDB data model for VitalSync with 3–5 collections. Include users, patients, appointments, and audit logs; specify key fields, references, indexes, validation rules, and relationship cardinalities. Use fictional data and minimize unnecessary health information. Output a Mermaid ER diagram and explain trade-offs. Do not generate database code.

**Purpose:** Plan persistence and references before backend implementation.

## Prompt 7 — QA demo script

> Create a maximum-three-minute QA walkthrough script for the VitalSync Sprint 13 planning deliverables. Demonstrate the README/PRD, desktop/tablet/mobile Figma views, architecture diagram, frontend state tree, API contracts, ERD, and Prompts.md. Clearly distinguish planned behavior from implemented behavior. Do not claim working features that are only designs.

**Purpose:** Keep the submission demo accurate and within the time limit.

## Assumptions to validate

- The project is on the Fullstack track.
- The four-collection MongoDB model is acceptable for the assignment.
- The proposed stack is permitted by the official brief.
- Figma sharing permissions allow reviewers to open the file.
- The exact due date and submission portal requirements match the official brief.

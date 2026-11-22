# From discovery to agent design: an AI-assisted rounding-note portfolio project

> **Synthetic data only. Not for clinical use.** This case study describes a product-learning project, not a deployed clinical system or validated agent.

## Summary

I explored how an AI-assisted copy-forward workflow could help hospitalists prepare an inpatient progress note before morning rounds. The intended workflow has two model responsibilities: a retriever selects relevant, current evidence; a documentation agent drafts a source-referenced SOAP note. The clinician remains responsible for review, edits, and signature.

The work covers the product lifecycle: discovery, ideation, workflow prototyping, synthetic-data preparation, requirements and evaluation planning, architecture, and an initial implementation. I used Codex as a build and thinking partner throughout. I did not fund live model inference, so the implementation has no successful model run and no measured quality, cost, or latency results.

## 1. Discovery and opportunity framing

The initial user group is hospitalists and physicians who create or review inpatient progress notes. The workflow enters before rounds: a clinician requests a draft, reviews and edits it, then signs. The feature does not sign on the clinician’s behalf or write to a real EHR.

I supplied planning assumptions of roughly 200 notes per day at one site and about 15 minutes per note. That implies approximately 50 staff-hours of note work per day if both assumptions hold. These figures are not measured baselines; clinician/SME validation remains outstanding.

**AI use:** Codex helped organize the discovery inputs into a durable artifact and calculate the implied aggregate time. It did not conduct user research or validate the assumptions.

**PM contribution:** I identified the intended users, workflow entry point, handoff to clinician review, and the need for SME/clinician approval. I kept volume and time labeled as assumptions rather than business-case facts.

## 2. Ideation and workflow prototyping

The concept evolved into **Copy Forward with AI** inside a simulated EHR Notes workflow. The prototype lets a reviewer explore the draft, inspect source references, edit, and see an unchanged prior-note fallback after simulated failure. PM feedback shaped selective phrase-level highlights: new or changed facts should be emphasized without tinting whole SOAP sections.

**AI use:** Codex generated and iterated on a local HTML/CSS/JavaScript prototype. The prototype uses hard-coded simulated results; it has no model or EHR connection.

**PM contribution:** I chose a high-fidelity clickable prototype, defined the key interactions and failure message, and reviewed the iterations. The prototype was accepted as a workflow-learning artifact, not as evidence of agent quality or clinical safety.

## 3. Synthetic data and evaluation preparation

The first fixture is a fictional 68-year-old inpatient on hospital day 3 for acute decompensated HFrEF. It contains a patient chart, a prior progress note, a handoff note, and a long-form transcript. The records deliberately distinguish current from discontinued orders, a one-time completed medication from a daily medication, direct measurement from recollection, pending from completed tests, and tentative discussion from an entered order.

The provisional golden set labels candidate facts as relevant or excluded. It is one scenario only, and its clinical labels have not been reviewed by an SME. The intended larger evaluation uses three scenarios, including traps and a clean case, with separate scoring for retrieval and documentation.

**AI use:** Codex helped author and inspect the synthetic source packet and draft provisional labels. No real patient data or employer product internals were used. No LLM judge was used.

**PM contribution:** I set the scenario purpose, identified the evaluation unit as a fact/statement, and assigned clinical ground-truth approval to SMEs rather than treating the PM or model as the clinical authority.

## 4. Requirements and product decisions

I set initial project targets of at least 95% retrieval recall, at least 95% retrieval precision, and zero unsupported clinical statements in evaluated drafts. I also specified a 10-second draft target, up to three retries after the initial attempt, and a fallback that displays the prior note unchanged with a clear failure message.

I chose to evaluate the retriever and documentation agent individually, then assess the end-to-end note. Component scoring helps locate whether a miss or distortion occurred during retrieval or drafting; end-to-end scoring checks the clinician-facing outcome. These targets and measures remain unevaluated.

I chose to retry only the failed agent, preserving successful work, with a shared retry cap. I chose not to buy API credits for this portfolio. The project therefore documents a no-paid-inference boundary and reports no model performance, token cost, or latency as achieved results.

**AI use:** Codex helped turn the product direction into requirements, explain API/SDK and cost concepts, and draft the implementation plan. I made the product choices and kept cost as a measurement to be learned rather than inventing a token budget before a PoC.

## 5. Architecture and implementation

The intended system has two model calls using the Responses API: a retriever returns a schema-constrained evidence packet, and a documentation agent returns a schema-constrained SOAP draft. Python code owns the orchestration, source-reference checks, retry policy, deadline, fallback, and JSONL logging. The UI prototype remains separate and simulated.

The initial code scaffold records per-agent attempts, latency, token usage, request IDs, retries, and outcome. It checks that cited source IDs are present in the fixture and that note statements cite IDs from the evidence packet. These checks support traceability; they do not establish that facts are clinically correct.

**AI use:** Codex drafted the Python code and reviewed the synthetic fixture distinctions while implementing it. The first in-sandbox launch could not reach the API. A network-enabled attempt reached the API but was rejected because the account had no credits. No model response was produced. The retry logic was then changed so billing/credit and authentication errors stop without repeated retries.

**PM contribution:** I kept the two-agent boundary explicit, chose retrying only the failed agent, chose no paid inference, and required that all limitations be visible in the portfolio. No EHR endpoint or real-patient-data path was added.

## 6. Evaluation status and honest limits

Evaluation is **not performed**. There are no successful agent outputs, clinician-reviewed labels, 15-run results, confusion matrices, cost-per-draft measurements, consistency results, or ship-gate verdict. The current fixture and labels do not support a clinical-quality or production-performance claim.

This project demonstrates product framing, design choices, a workflow prototype, an agent architecture, and an evaluation plan. It does not demonstrate that the model agents meet their targets. That distinction is central to the portfolio: planned thresholds are not results.

## What I would do next

If the project later receives a funded test budget and clinician/SME time, I would first complete the three-scenario golden set and label review, then run a small controlled PoC to measure per-agent latency, token usage, retries, and failure behavior. I would compare those observations with the 10-second target and cost assumptions before deciding whether a larger evaluation is justified. The workflow prototype and the agent implementation would remain separately identified.

## Supporting artifacts

- [Discovery notes](discovery.md)
- [Requirements and evaluation plan](requirements.md)
- [Decision log](decisions.md)
- [Synthetic case 001](../data/synthetic_case_001/README.md)
- [Provisional golden set](golden-set.md)
- [Workflow prototype](../prototype/index.html)
- [Prototype review notes](prototype-notes.md)
- [Implementation notes](implementation-notes.md)
- [Evaluation status](eval-results.md)

# Initial Product Requirements and Evaluation Plan

**Status:** Draft from product discovery; functional scope and numeric targets require clinician/SME review.

## Product goal and user

Help a hospitalist or physician prepare an inpatient progress note before rounds. The clinician reviews and signs the draft. Synthetic data only; no EHR write-back.

## Use case

A clinician selects **Progress Notes with AI**. The system generates a draft progress note using relevant patient context from:

- The patient's transcript, either manually documented in the EHR or produced by speech-to-text.
- Previous progress notes.
- Handoff notes.
- Updates documented within the configured past-24-hour window.

The AI-generated draft may preserve prior information only when it remains relevant and supported. Changed, contradicted, or stale statements must be updated or removed; copying prior text forward without checking it is not acceptable. Every clinical statement should be traceable to its source, and missing or conflicting information should be surfaced for clinician review.

**Failure-path exception:** If AI context retrieval/note generation still fails after the allowed retries, the system may present the previous day's note as an unchanged copy-forward draft, without additional context retrieval or AI edits. It must clearly tell the clinician that retrieval/generation failed and that the displayed note was not updated; the clinician reviews and edits it before signing.

## Initial functional requirements

1. Let the clinician initiate progress-note generation from the progress-notes workflow.
2. Retrieve the transcript, prior progress notes, and handoff notes available for the synthetic patient.
3. Identify relevant updates in the configured 24-hour window.
4. Produce a structured progress-note draft from supported context.
5. Preserve still-current prior context only when supported; update or remove stale or contradicted content.
6. Make source references available for note statements and flag missing or conflicting context.
7. Present the draft for clinician review and signature; the system does not sign on the clinician's behalf.
8. Retry failed note-generation attempts up to three times. If all retries fail, present the previous day's note unchanged as the non-AI copy-forward fallback, without retrieving or adding context. Clearly tell the clinician that context retrieval/note generation failed and that the copied note was not updated; keep it in the clinician review/signature workflow.

These are starting requirements, not a complete specification. Detailed acceptance criteria will be added where they help evaluate the behavior being built.

## AI-assisted rapid-prototyping phase

**Status:** Complete as of 2026-11-18. The high-fidelity local clickable workflow prototype was reviewed by the PM and accepted. See [the prototype review record](prototype-notes.md). The next phase is implementation of the retrieval and documentation agents, separately from the prototype.

Before implementing the retrieval and documentation agents, build a small, local, clickable prototype to explore the clinician workflow. The prototype should use only the existing fictional case and simulated retrieval/drafting results; it is for learning and workflow feedback, not a production system or a clinical quality evaluation.

The prototype should let a reviewer explore the main path (request a SOAP progress-note draft, review the draft and source references) and the failure path (show retrieval/generation failure and the previous-day note copy-forward fallback with a clear warning). Keep it separate from production agent logic and real API/EHR integrations. Use the simplest maintainable prototyping approach available in the repository, and explain the trade-offs as part of the learning process.

The rapid-prototyping deliverable is a reviewable local prototype plus a short record of what workflow questions it helps answer and what changed after review. It does not replace or count as implementation of the two agents.

## Non-functional requirement areas

- **Performance:** Provide the requested progress-note draft within 10 seconds of the clinician's request. The retry behavior must be evaluated against this end-to-end limit; engineering feasibility is still to be confirmed.
- **Security and privacy:** synthetic data only for this portfolio; protect credentials; no real EHR integration.
- **Traceability and auditability:** retain source IDs and run traces sufficient to inspect retrieval, drafting, and evaluation outcomes.
- **Reliability:** handle missing or conflicting sources without inventing information; retry failed generation up to three times, then provide the clearly identified previous-day copy-forward fallback and retrieval-failure message.
- **Usability:** clinician can review, understand, and edit the draft before signing.

Numeric thresholds and detailed controls remain to be decided with clinician/SME input.

## Product metrics and agent evaluations

### Product-level metrics

- Progress-note content quality/accuracy, graded against a clinician-reviewed reference.
- Time to produce a draft, with clinician review/edit time measured separately where possible.

### Agent-level metrics

- **Recall:** expected relevant context items retrieved ÷ all expected relevant context items.
- **Precision:** retrieved context items judged relevant ÷ all retrieved context items.
- **Accuracy:** (true positives + true negatives) ÷ all labeled items. This requires a defined set of relevant and irrelevant candidate facts; raw free-text context makes true negatives ambiguous.

### Project evaluation targets

- **Retrieval recall:** ≥95% on the labeled relevant fact items.
- **Retrieval precision:** ≥95% on the labeled evaluation set.
- **Unsupported statements in the generated note:** 0% in evaluated drafts; each clinical statement must be supported by the evidence passed to the documentation agent and traceable to a source.
- These are PM-selected targets for this training project. They are evaluation acceptance targets, not evidence of production-level performance; that claim would require sufficiently large and representative data. See `docs/decisions.md`.

Evaluate retrieval and final note quality separately so a retrieval miss can be distinguished from a drafting error. Use code checks for deterministic requirements and clinician review for clinical quality; no LLM judge is assumed at this stage.

## Evaluation design: define now, build later

The requirements phase should specify the evaluation unit, labels, metrics, thresholds, graders, and release gate. The golden-set scenarios and confusion-matrix approach are part of this evaluation design.

The actual golden-set charts, traps/decoys, source IDs, ground truth, validation, repeated runs, scoring, and error analysis are later data-preparation and evaluation work. Define expected fact items and grading rules before building the scenarios so that results are not scored against a moving target.

Planned evaluation elements:

- Golden set of three scenarios, including trap variants and a clean scenario to measure false positives.
- Fact-level labels for expected relevant items and decoys; confusion matrices can then report TP, FN, FP, and TN.
- Separate retrieval metrics from note-level correctness, source traceability, stale carry-forward, and conflict handling.
- Numeric KPI targets, grader responsibilities, and ship gate: TBD.

## Open decisions

- Accuracy target (if accuracy remains a required KPI), cost/latency budgets, and any separate critical-category gates.
- Engineering feasibility of the 10-second end-to-end target with up to three retries; determine the exact timeout and retry policy.
- Error severity and blocker/non-blocker classification; decide after reviewing the first evaluation results.
- Whether transcript means one encounter transcript or multiple transcript records across the time window.
- Exact note structure and clinician review workflow.
- Clinician-approved definition of relevant context and the golden-set fact-level rubric.
- SME/clinician approval of scope, safety stance, and acceptance criteria.

## PM-owned golden-set work (agreed 2026-11-17)

- The PM defines the product evaluation question and unit: one distinct candidate fact or statement assessed for whether it should be passed to the note-writing agent.
- The PM defines the expected dataset shape and makes sure the set can support the agreed metrics and error analysis.
- The PM coordinates scope and coverage: which scenarios, source types, and important failure situations must be represented; clinical SMEs determine and validate clinical coverage.
- Clinical SMEs create or enter the expected labels and resolve clinical disagreements. The PM does not independently decide clinical ground truth or label the full clinical dataset.
- The PM tracks whether SME review is complete and whether the set is fit for the planned evaluation. The actual labels remain clinician-owned.

The first provisional labels and coverage review are in [docs/golden-set.md](golden-set.md). They are drafted from this project's synthetic fixture and are not clinician-approved ground truth.

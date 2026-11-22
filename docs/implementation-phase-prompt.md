# Next phase prompt: implement the inpatient rounding agents

Copy this prompt into the next implementation session.

---

The AI-assisted rapid-prototyping phase is complete. The local, high-fidelity, clickable clinician workflow prototype was reviewed and accepted. The next action is to begin the separate implementation phase for the two agents: retrieval and SOAP documentation.

## Project context

This project explores helping a hospitalist or physician prepare an inpatient progress note before rounds. The clinician must review, edit, and sign the note. The system must never sign on the clinician's behalf.

The eventual system has two distinct agent responsibilities:

1. **Retrieval agent:** select relevant evidence from the available synthetic chart, prior progress notes, handoff notes, and transcript for the configured past-24-hour window. Return evidence with source references and enough provenance to inspect timestamps and status. Identify missing, stale, superseded, or conflicting information; do not convert tentative discussion into an order.
2. **Documentation agent:** format supported evidence into a structured SOAP draft. Carry forward prior note content only when it remains current and supported. Update or remove changed, contradicted, or stale content. Make every clinical statement traceable to its source and surface uncertainty or conflicts for clinician review.

The workflow entry point is the EHR's existing copy-forward action relabeled **Copy Forward with AI**. The clinician requests a draft, reviews its source references and selectively highlighted new or changed phrases, edits it, and signs it. Most of the prior SOAP note may remain unchanged; highlights should point to specific updated content rather than tinting entire sections.

## Failure and performance requirements

- Target a draft within 10 seconds of the clinician request; engineering must determine whether the end-to-end budget can include retries.
- On failure, retry up to three times after the initial attempt.
- If retrieval or generation still fails, show the previous day's note unchanged as the non-AI fallback. Do not add retrieved context or AI edits on this path.
- Clearly state that context retrieval/note generation failed and that the displayed note was not updated. Keep the fallback in the clinician review/edit/sign workflow.

## Source data and case facts

Use only the fictional data in `data/synthetic_case_001/`. Read all of these before implementation:

- `data/synthetic_case_001/README.md`
- `data/synthetic_case_001/patient_chart.md`
- `data/synthetic_case_001/prior_progress_note.md`
- `data/synthetic_case_001/handoff_note.md`
- `data/synthetic_case_001/transcript.md`

The note reference time is **2026-11-17 07:30 UTC**. The previous note was signed **2026-11-16 06:10 UTC**. The fixture includes current and stale medication orders, new labs and weights, patient-reported symptoms, I/O, a pending ambulatory oxygen check, an imprecise handoff weight recollection, and a tentative medication discussion. Preserve timestamps, source identity, attribution, and status.

Important fixture distinctions:

- Active inpatient furosemide is **80 mg IV every 12 hours**. The home dose is **40 mg PO once daily**. The old 40 mg IV q12h order was discontinued. There is no source for a 100 mg q12h order or decision.
- Metolazone was discussed as a possible future option only; no order was entered and no dose was given.
- The one-time potassium chloride 20 mEq dose on 2026-11-16 was completed; do not turn it into a daily medication.
- The current morning standing weight is 90.2 kg at 05:55; the handoff's “about 91 kg” was an unmeasured rounded recollection. Prior morning weight was 90.9 kg at 06:05 on 2026-11-16; evening weights are separate readings.
- Current labs at 05:00 include potassium 3.8 mmol/L and creatinine 1.49 mg/dL. Keep values, units, and times attached; baseline creatinine is reported as 1.3–1.5 mg/dL.
- The 24-hour I/O interval 2026-11-16 06:00–2026-11-17 06:00 records 1,520 mL intake, 2,280 mL urine output, net −760 mL.
- An ambulatory oxygen saturation check is ordered for 09:00 and is pending at the note reference time. Do not invent a result.
- Similar JVP/crackles appeared in the prior-day note and were observed again on the 07:02 exam. Distinguish a new timestamped observation from a claim that the finding was never previously documented.

## Evaluation targets and limits

- Retrieval recall target: **≥95%**.
- Retrieval precision target: **≥95%**.
- Unsupported clinical statements in evaluated drafts: **0%**.
- These are project evaluation targets, not achieved results or a production-quality claim.
- The current golden set in `docs/golden-set.md` is a **one-scenario draft with provisional labels**. It has not been clinically validated. Do not describe it as clinician-approved ground truth or use it to claim agent quality.
- Keep retrieval evaluation separate from note-level correctness, source traceability, stale carry-forward, and conflict handling. Clinician/SME review is needed for clinical labels and quality claims.
- The golden-set plan calls for three scenarios, including traps and a clean scenario; coverage, labels, grader roles, and ship gate remain open.

## Privacy, integration, and implementation boundaries

- Synthetic data only. Do not use real patient information, a real EHR, production credentials, or a production API.
- Keep the existing prototype at `prototype/index.html` as a separate workflow artifact. It uses hard-coded simulated results and is not the agent implementation.
- Inspect the repository before choosing a framework. There is no application framework at the project root; avoid adding infrastructure until the implementation requires it.
- Do not make unsupported clinical assumptions. If required behavior is ambiguous, document the assumption and keep source-grounded logic separate from clinical decisions that need SME input.
- Do not present prototype behavior as implementation, model evaluation, or clinical validation.

## Start implementation

Read the project requirements, decisions, golden set, prototype review notes, and synthetic sources. Then proceed with implementing the retrieval and documentation agent responsibilities as a separate, reviewable phase. Preserve evidence provenance end to end, make failure handling explicit, and document implementation choices and any unresolved engineering or clinical questions in the project docs. Do not claim that the numeric targets are met until a suitable evaluation has been run on an adequately reviewed set.

Project references:

- `docs/requirements.md`
- `docs/decisions.md`
- `docs/golden-set.md`
- `docs/prototype-notes.md`
- `prototype/index.html`

---

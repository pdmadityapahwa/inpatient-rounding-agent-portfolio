# Project decisions

## D-001 — Retrieval recall target

- **Date:** 2026-11-17
- **Decision:** Set retrieval recall target at ≥95% for this project.
- **Options discussed:** 90%, 95%, or 98% recall.
- **Choice:** 95%, selected by the PM. The PM briefly raised this to 98%, then returned it to 95%.
- **Why:** The PM wants high retrieval coverage while balancing it with precision. This is a product acceptance choice, not a percentage calculated from the dataset.
- **Owner:** PM selection; Codex recorded the choice.
- **Status:** Project target. The current small, single-patient synthetic set cannot support a production performance claim.

## D-002 — Retrieval precision target

- **Date:** 2026-11-17
- **Decision:** Set retrieval precision target at ≥95% for this project.
- **Options discussed:** Precision threshold not previously set; the PM first chose 100%, then lowered it to 95%.
- **Choice:** 95% precision on the labeled evaluation set.
- **Why:** The PM considers some additional context acceptable in the draft, while still requiring most passed items to be relevant. This is a product acceptance choice, not a percentage calculated from the dataset.
- **Owner:** PM selection; Codex recorded the choice.
- **Status:** Project target. The current small, single-patient synthetic set cannot support a production performance claim.

## D-003 — Unsupported statements in the generated note

- **Date:** 2026-11-17
- **Decision:** Target zero unsupported clinical statements in evaluated note drafts.
- **Choice:** 0% unsupported-statement rate for the evaluation examples; every clinical statement must be supported by the evidence packet and traceable to a source.
- **Why:** The PM stated that hallucinations should not occur. This is separate from retrieval precision: a retrieved item may be relevant while the drafter could still add an unsupported claim.
- **Owner:** PM requirement; Codex recorded the interpretation as an evaluation target.
- **Status:** Project target. Grading method and source-trace check still need to be applied during evaluation.

## D-004 — End-to-end completion and retry behavior

- **Date:** 2026-11-17
- **Decision:** Target a progress-note draft within 10 seconds of the clinician's request. On failure, retry up to three times after the initial attempt. If generation still fails, present the previous day's note unchanged as a non-AI fallback, without additional retrieval, and tell the clinician context retrieval/note generation was unsuccessful.
- **Choice:** The PM specified the 10-second maximum, up to three retries, and previous-day copy-forward fallback.
- **Why:** The clinician should receive a timely draft or a clearly identified fallback and failure message. Copy-forward is common in the described workflow; the fallback must not imply that today's context was retrieved or the note was updated.
- **Owner:** PM selection; engineering must confirm timing and retry feasibility.
- **Status:** Fallback behavior recorded. Engineering must confirm whether the 10-second limit can cover all retries and define the timeout implementation. The copied note remains subject to clinician review before signing.

## D-005 — Error severity and release blockers

- **Date:** 2026-11-17
- **Decision:** Defer blocker/non-blocker classification until after the first evaluation run.
- **Choice:** Review observed errors and then decide their severity and release impact.
- **Why:** The PM wants to base the classification on actual test failures rather than assign categories before seeing system behavior.
- **Owner:** PM decision; Codex recorded it.
- **Status:** Deferred until initial evaluation results are available.

## D-006 — Add AI-assisted rapid prototyping before agent implementation

- **Date:** 2026-11-18
- **Decision:** Add a rapid-prototyping phase before building the retrieval and documentation agents.
- **Choice:** Create a local, clickable workflow prototype using the fictional source packet and simulated agent results; do not connect it to a real EHR or production model/API.
- **Why:** The PM wants to learn and use AI-assisted prototyping to explore the clinician workflow before implementing the agent system.
- **Owner:** PM requested this scope; Codex recorded the decision.
- **Status:** Complete. Clickable prototype built, reviewed, and accepted; see [docs/prototype-notes.md](prototype-notes.md).

## D-007 — Start with a high-fidelity clickable EHR workflow prototype

- **Date:** 2026-11-18
- **Decision:** Begin directly with a high-fidelity, clickable desktop EHR-style prototype rather than making a low-fidelity prototype first.
- **Choice:** Simulate the clinician's existing Notes workflow with a **Copy Forward with AI** action, editable SOAP note, selective highlights on new or updated phrases, clickable source references, and a failure control that shows the prior note unchanged with a clear warning.
- **Why:** The PM wants to practice high-fidelity clickable prototyping and explore how the feature could appear in the EHR context. A static image would not demonstrate the interaction or the failure state.
- **Constraints:** Local, fictional data only; no EHR, AI API, or real agent logic. This interface is a learning artifact and does not establish clinical validity or product performance.
- **Owner:** PM direction; Codex recorded and prototyped the decision.
- **Status:** First clickable iteration reviewed; follow-up change recorded in D-008.

## D-008 — Highlight selective note changes, not whole SOAP sections

- **Date:** 2026-11-18
- **Decision:** In the prototype, highlight only the specific new or updated phrases and values; leave unchanged copy-forward text unhighlighted.
- **Choice:** The successful path shows selective highlights for current timestamped exam and measurements, new pending test context, and unresolved discharge-dose status. The failure path continues to display only the prior note unchanged.
- **Why:** PM review clarified that most of the note is expected to carry forward and the visual signal should identify the changed content at phrase level.
- **Source integrity:** Do not present a medication-dose change as retrieved context unless the fictional source packet contains that order/decision. The current case supports furosemide 80 mg IV every 12 hours; it does not support an increase to 100 mg.
- **Owner:** PM feedback; Codex recorded and applied the choice.
- **Status:** Applied and accepted by PM. Prototype phase complete; next phase is agent implementation.

## D-009 — Retry only the failed agent

- **Date:** 2026-11-21
- **Decision:** If an agent call fails, retry that agent without rerunning an agent that already succeeded.
- **Options discussed:** Retry only the failed agent; restart the full two-agent sequence.
- **Choice:** Retry only the failed agent.
- **Why:** This preserves successful work and avoids repeated model calls when the documentation agent fails after retrieval. The existing cap of three retries after the initial attempt remains shared across the run and subject to the 10-second deadline.
- **Owner:** PM selection; Codex recorded and implemented the decision.
- **Status:** Implemented in the local prototype code; runtime behavior remains unevaluated.

## D-010 — Skip paid live model evaluation for the portfolio

- **Date:** 2026-11-21
- **Decision:** Do not purchase API credits or make paid live model calls for this portfolio project.
- **Options discussed:** Fund API usage and run the agents; stop live inference and present the architecture, PM decisions, and evaluation plan without claiming measured model performance.
- **Choice:** Skip paid inference and actual model evaluation.
- **Why:** The portfolio goal is to demonstrate product and agentic-architecture understanding, including explicit decisions and evaluation design. Paying for model calls is outside the chosen scope.
- **Owner:** PM decision; Codex recorded it.
- **Status:** Adopted. The API-backed code remains an unexecuted implementation artifact; performance and quality targets are not evaluated.

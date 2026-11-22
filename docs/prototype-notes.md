# Clinician workflow prototype

**Status:** Complete; PM reviewed and accepted iteration 2  
**Date started:** 2026-11-18  
**Prototype:** [`prototype/index.html`](../prototype/index.html)

## Purpose

Explore how a clinician might use an AI-assisted copy-forward workflow inside a desktop EHR context. The prototype is intended to make the note review, update highlighting, source lookup, and fallback experience tangible before the separate retrieval and documentation agents are implemented.

This is a local learning artifact. It uses only the fictional synthetic case and hard-coded simulated responses. It is not connected to a model/API or EHR, does not retrieve data, and does not create a clinical note. Nothing is saved or signed outside the browser interaction. It is not a clinical quality evaluation.

## Initial question

Can a clinician distinguish carried-forward SOAP text from selectively highlighted new or changed phrases, inspect the source behind an update, and recognize that the fallback note is unchanged when retrieval fails?

## Key decisions

- Start directly at high fidelity, per PM direction, using an EHR-like desktop chart frame rather than a standalone chat assistant.
- Keep **Copy Forward with AI** as the workflow entry point in the Notes screen.
- Present the SOAP note as an editable draft. Highlight only the specific phrases and values with simulated updates; leave unchanged copy-forward content unhighlighted. Expose linked source references alongside the content.
- Provide a simulated failure control. It represents one failed initial attempt plus three retries, then shows the previous note unchanged with a prominent context-retrieval warning.
- Include simulated edit and sign controls to explore the user journey; these controls do not save or sign a real note.
- Use one standalone HTML file with inline CSS and JavaScript because the repository has no existing app framework or build setup. Trade-off: quick to open and modify, but not componentized and not suitable as production architecture.
- Label the prototype visibly as fictional, simulated, and not for clinical use.

## First iteration review log

| Review | Findings | Change / next action |
|---|---|---|
| Source review by Codex | The case includes current exam and symptoms, timestamped weight, laboratory values, I/O, a pending ambulatory oxygen check, and unresolved discharge medication planning. | Included these as simulated note updates with source links. Kept metolazone out of the note as it was discussion-only. |
| Implementation review by Codex | The failure path must preserve the prior note content and say it was not updated. The requirements specify up to three retries after the first attempt. | Failure state shows the unchanged prior note and explicitly says initial attempt plus 3 retries failed. |
| PM feedback, iteration 2 | Highlight only selective additions/updates; most of the SOAP note should remain ordinary copy-forward text. The PM suggested current JVP/crackles, reassessing congestion/oral transition, and increasing furosemide to 100 mg every 12 hours. | Updated the successful draft to highlight phrases and current values rather than entire SOAP sections; failure still renders only the prior note. The prior note includes similar JVP/crackles findings, so the prototype labels the 07:02 current exam observation with its timestamp rather than suggesting those findings were never documented. The prior note already says to reassess congestion and oral transition, so that plan remains unhighlighted. The source packet has no 100 mg order or decision; retained the sourced active 80 mg IV q12h regimen and did not portray a dose increase as retrieved evidence. Highlighted current weight/lab/I&O values, the pending ambulatory oxygen check, and the undecided discharge regimen instead. |
| PM visual / workflow review | PM reviewed iteration 1, requested selective phrase-level highlighting, reviewed iteration 2, and accepted the prototype as complete. | Prototype phase complete. The requested 100 mg q12h dose escalation was not added because no such order or decision exists in the selected synthetic case. |

## Handoff

The next project phase is implementation of the retrieval and documentation agents as a separate workstream. See the copy-ready [implementation phase prompt](implementation-phase-prompt.md).

## Claims and limitations

The project's 95% retrieval recall, 95% precision, and zero unsupported clinical statements are evaluation targets for later evaluation. This prototype has no measured retrieval or note-generation performance. The current golden set is a one-scenario draft with provisional labels and has not been clinically validated.

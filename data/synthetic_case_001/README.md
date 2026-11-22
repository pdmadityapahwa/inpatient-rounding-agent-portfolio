# Synthetic inpatient case 001

**Status:** Draft source packet for evaluation-data preparation. Everything in this folder is fabricated. It is not derived from a real patient or real EHR export and is not for clinical use.

## Scenario

Fictional 68-year-old inpatient, hospital day 3, admitted with acute decompensated heart failure with reduced ejection fraction (HFrEF). The note-generation reference time is 2026-11-17 07:30 UTC. The prior progress note was signed 2026-11-16 06:10 UTC. The source window includes events before and after that note so the evaluator can distinguish prior context from new events.

## Files

- `patient_chart.md` — structured patient profile, problem list, medication history, orders, vitals, labs, imaging, and intake/output.
- `prior_progress_note.md` — the prior-day note, timestamped 2026-11-16 06:10 UTC.
- `handoff_note.md` — shift handoff with both useful facts and an explicitly unresolved discussion.
- `transcript.md` — fabricated speech-to-text style record of patient, family, and care-team conversations. It is intentionally long-form and contains repeated, irrelevant, superseded, and potentially conflicting statements for evaluation.

## Clinical reference basis

This scenario uses common inpatient heart-failure concepts as plausibility checks, not as treatment advice. The AHA/ACC/HFSA guideline discusses IV loop diuretics for hospitalized patients with significant fluid overload and reassessment of congestion. See the [2022 AHA/ACC/HFSA Heart Failure Guideline](https://professional.heart.org/-/media/832EA0F4E73948848612F228F7FA2D35.pdf). The [ACC hospitalized heart-failure pathway](https://www.acc.org/About-ACC/Press-Releases/2024/08/08/18/29/American-College-of-Cardiology-Issues-Guide-for-Managing-In-Patient-Heart-Failure) gives a contemporary overview of inpatient decision-making.

The chart is authored as a readable EHR-style fixture rather than a standards-compliant FHIR bundle. The [FHIR Observation resource](https://hl7.org/fhir/R4/observation.html), [Condition resource](https://hl7.org/fhir/R4/condition.html), and [MedicationRequest resource](https://hl7.org/fhir/R4/medicationrequest.html) are useful references for the kinds of fields a structured export may contain.

## Important limitations

This is a first synthetic draft. Drug doses, trends, and internal consistency are intended to be plausible, but a clinician must review the packet before any clinical-accuracy claim or final ground-truth labels are made. Do not use these artifacts to guide care. The evaluation labels are deliberately not included here so the reviewer can independently identify expected inclusions and exclusions.

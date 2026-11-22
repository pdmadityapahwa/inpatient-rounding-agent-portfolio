# Golden set — first synthetic case

**Version:** 0.1 draft  
**Status:** Provisional labels; clinical SME review required  
**Date:** 2026-11-17  
**Use:** Practice dataset for the retrieval agent in the synthetic inpatient-rounding project. Not for clinical use.

## PM-owned definition

- **Evaluation unit:** one distinct candidate fact or statement from the supplied sources.
- **Expected decision:** `PASS` means provide the item to the note-writing agent as relevant evidence for the 2026-11-17 07:30 UTC note. `EXCLUDE` means do not pass it as note evidence (for example, it is irrelevant, tentative discussion, superseded, or an imprecise recollection).
- **Time scope:** events after the prior note signed at 2026-11-16 06:10 UTC, plus older context that remains relevant to today's note.
- **Clinical ground truth:** the `PASS`/`EXCLUDE` values below are provisional, drafted from the synthetic case by Codex. A clinician/SME must validate, change, or reject them before this is called an approved golden set.

The PM-owned definition is the product/evaluation contract. Clinical SMEs own the clinical correctness of the labels and the final clinical coverage decision. This draft does not imply a clinician has reviewed it.

## Provisional labeled examples

The `#` column is only a row reference for discussion. It is not a separate case ID or an additional clinical concept.

| # | Candidate information item | Source | Expected decision | Provisional rationale |
|---:|---|---|---|---|
| 1 | HFrEF with most recently documented LVEF approximately 30%; the 2026-11-15 echo is similar to the August study. | `patient_chart.md`, imaging/history; `transcript.md`, TX-011 | PASS | Relevant current diagnosis and cardiac function context. |
| 2 | Admission was for acute decompensated HFrEF with fluid overload after several days of dyspnea, orthopnea, edema, and weight increase. | `patient_chart.md`, Presenting history | PASS | Relevant context for today's progress note, summarized without repeating the full admission narrative. |
| 3 | Patient reports missing two home furosemide doses because of a pharmacy refill delay; home regimen is 40 mg PO once daily. | `patient_chart.md`, Home medications; `handoff_note.md`, Background; `transcript.md`, TX-002/TX-021 | PASS | Relevant precipitating/context information and needed distinction between home and inpatient doses. |
| 4 | Current inpatient furosemide order is 80 mg IV every 12 hours. | `patient_chart.md`, Current and recent medication orders; `handoff_note.md`, Background; `transcript.md`, TX-010/TX-029 | PASS | Current active treatment; include route and frequency. |
| 5 | The initial furosemide 40 mg IV every 12 hours order was discontinued on 2026-11-15 and replaced by 80 mg IV every 12 hours. | `patient_chart.md`, Current and recent medication orders; `transcript.md`, TX-010 | EXCLUDE | The old dose is historical and predates the prior note. Do not pass it as current medication context; the active 80 mg IV order is listed separately. |
| 6 | One-time potassium chloride 20 mEq PO dose was ordered and completed on 2026-11-16 at 14:05. | `patient_chart.md`, Current and recent medication orders; `transcript.md`, TX-020 | PASS | A treatment event after the prior note that may be relevant to the interval and potassium trend; preserve that it was one-time and completed, not a chronic medication. SME to confirm note-worthiness. |
| 7 | The team discussed possible metolazone on 2026-11-16 but made no decision and entered no order. | `handoff_note.md`, Unresolved discussion; `patient_chart.md`, Active orders; `transcript.md`, TX-022/TX-023/TX-031 | EXCLUDE | Exclude as an order or treatment plan. This is tentative discussion only. If the product requirement includes reporting material unresolved discussion, SME should revise this label/rule explicitly. |
| 8 | Empagliflozin is held during acute illness and should be reassessed before discharge. | `patient_chart.md`, Current and recent medication orders; `prior_progress_note.md`, Plan | PASS | Relevant medication status and future reassessment; preserve that it is held, not active. This hold predates the prior note. |
| 9 | Metformin ER 500 mg twice daily is held during the inpatient stay. | `patient_chart.md`, Home medications and current orders | PASS | Relevant medication status if the note includes inpatient diabetes management; clinician should confirm whether it belongs in this day's note. |
| 10 | Morning standing weight on 2026-11-17 at 05:55 was 90.2 kg. | `patient_chart.md`, Vitals; `handoff_note.md`, Situation/Assessment; `transcript.md`, TX-027/TX-030 | PASS | Most recent timestamped weight; retain time and standing-scale method. |
| 11 | A handoff recollection said “about 91 kg,” without a new measurement; the precise 05:55 standing weight was 90.2 kg. | `handoff_note.md`, Handoff caveat; `transcript.md`, TX-028 | EXCLUDE | Do not pass the rounded recollection as today's measured weight. The discrepancy and its provenance can be surfaced if the system is required to flag conflicting sources. |
| 12 | Prior morning standing weight was 90.9 kg on 2026-11-16 at 06:05. | `patient_chart.md`, Vitals; `prior_progress_note.md`, Objective; `transcript.md`, TX-016 | PASS | Relevant comparator for today's morning weight trend; include date/time so it is not confused with the evening value. |
| 13 | Evening weight was 90.8 kg on 2026-11-16 at 17:55. | `patient_chart.md`, Vitals; `handoff_note.md`, Situation; `transcript.md`, TX-024 | PASS | Relevant but distinct from morning weights. Preserve timestamp; do not use it as the current morning measurement. |
| 14 | Intake was 1,520 mL and urine output 2,280 mL from 2026-11-16 06:00 to 2026-11-17 06:00; recorded net balance −760 mL. | `patient_chart.md`, Intake and output; `handoff_note.md`, Assessment; `transcript.md`, TX-027 | PASS | Relevant last-24-hour treatment response, with interval and measured/recorded status retained. |
| 15 | Potassium was 3.8 mmol/L and creatinine 1.49 mg/dL on 2026-11-17 at 05:00. | `patient_chart.md`, Laboratory results; `handoff_note.md`, Assessment; `transcript.md`, TX-026 | PASS | Current labs relevant during IV diuresis and after potassium replacement. Keep values, units, and time attached. |
| 16 | Creatinine changed from 1.52 mg/dL on 2026-11-16 to 1.49 mg/dL on 2026-11-17, with reported baseline 1.3–1.5 mg/dL. | `patient_chart.md`, Laboratory results/history; `prior_progress_note.md`, Assessment; `transcript.md`, TX-016/TX-026 | PASS | Relevant trend and baseline context; avoid describing this small change as a major improvement. |
| 17 | Patient reports breathing is improved at rest but still has mild dyspnea walking to the bathroom. | `handoff_note.md`, Situation/Assessment; `transcript.md`, TX-027/TX-029/TX-031 | PASS | Current symptom and functional status. Attribute as patient report. |
| 18 | Patient denies chest pain, fever, new cough, and dizziness during the 2026-11-17 morning review. | `transcript.md`, TX-029 | PASS | Pertinent current negatives for the assessment; keep attributed to patient report. |
| 19 | Oxygen saturation was 96% on room air at rest on the morning of 2026-11-17. | `patient_chart.md`, Vitals; `transcript.md`, TX-029/TX-030 | PASS | Current objective status; distinguish resting saturation from the ambulatory check that is still pending. |
| 20 | Ambulatory oxygen saturation check is ordered for 09:00 on 2026-11-17 and has not yet been completed at the 07:30 reference time. | `patient_chart.md`, Active orders; `handoff_note.md`, To do / watch; `transcript.md`, TX-030 | PASS | Pending task relevant to today's plan. Do not invent a result. |
| 21 | Trace bilateral ankle edema and faint bibasilar crackles were noted on the 2026-11-17 exam. | `transcript.md`, TX-030 | PASS | Current exam findings relevant to residual congestion. |
| 22 | No acute overnight event or chest pain was reported; no overnight arrhythmia event was reported by nursing. | `handoff_note.md`, Situation/Assessment | PASS | Relevant overnight interval status, attributed to report rather than treated as a definitive rhythm interpretation. |
| 23 | Lisinopril caused a persistent dry cough; allergy history was confirmed by the patient. | `patient_chart.md`, Allergies and reactions | PASS | Relevant medication safety context if medication choices are discussed; preserve reaction and source. SME to confirm inclusion in today's note. |
| 24 | Patient has CKD stage 3a with reported creatinine baseline 1.3–1.5 mg/dL. | `patient_chart.md`, Medical history; `prior_progress_note.md`, Assessment | PASS | Relevant to interpreting current renal function and diuresis. |
| 25 | Patient's home scale reportedly read about 203 lb on the morning of admission. | `transcript.md`, TX-001/TX-004 | EXCLUDE | Historical, patient-reported, and superseded by several timestamped inpatient weights for today's status. It may be relevant to admission history but not a current weight. |
| 26 | Patient may try CPAP later; use at home is inconsistent. | `patient_chart.md`, Medical history; `transcript.md`, TX-007 | EXCLUDE | Not a current change or issue addressed in today's plan; not needed in this note unless the clinician identifies a current respiratory/OSA concern. |
| 27 | Patient ate a few crackers brought by family before the diet change; sodium amount is unknown. | `transcript.md`, TX-012 | EXCLUDE | No reliable sodium quantity and no specific current assessment decision. Do not infer an amount or causal link. |
| 28 | Patient completed a 30-meter walk on 2026-11-15 while receiving 1 L/min oxygen, with saturation 94% after walking. | `transcript.md`, TX-013 | EXCLUDE | Older mobility data from 2026-11-15; today's ambulatory oxygen assessment is pending. Avoid presenting it as current. |
| 29 | The patient asked whether he would return to 40 mg oral furosemide at discharge; no final discharge regimen has been decided. | `transcript.md`, TX-031; `handoff_note.md`, To do / watch | PASS | Relevant unresolved discharge planning, stated as undecided; do not turn the home dose into a discharge order. |
| 30 | Current active medication list includes sacubitril/valsartan 49/51 mg PO twice daily, carvedilol 12.5 mg PO twice daily, spironolactone 25 mg PO daily, apixaban 5 mg PO twice daily, and atorvastatin 40 mg nightly. | `patient_chart.md`, Current and recent medication orders | PASS | Current medication context may support the plan; include only to the degree relevant to today's assessment and avoid copying the entire list into the note without a purpose. |

## Coverage checklist

This first case draws examples from the patient chart, prior progress note, handoff note, and transcript. It includes current and stale medication status, a new one-time order after the prior note, discussion without an order, current and historical weights, patient-reported versus measured information, a pending test, current symptoms and exam findings, and an older mobility result.

It is **not yet the full evaluation set defined in the project brief**. Only one scenario exists. The required post-note medication discontinuation that remains stale in the prior note is not represented. The required lab trend that clearly contradicts the prior note's narrative is not represented. The weight discrepancy is explicitly reconciled in the source material, so it is a mild provenance case rather than an unresolved conflict. Scenarios 2 and 3, trap variants, and clinician-approved labels remain to be created.

## Review log

| Review field | Status |
|---|---|
| Draft label author | Codex, from project synthetic source files |
| Clinical SME reviewer | Not yet assigned |
| Clinical label approval | Pending |
| Coverage approval | Pending |
| Numeric KPI targets / ship gate | Not set |

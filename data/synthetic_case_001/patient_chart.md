# Patient chart — synthetic case 001

> **FICTIONAL DATA — NOT FOR CLINICAL USE.** All identifiers and events are invented.

## Patient and encounter

| Field | Value |
|---|---|
| Patient ID | SYN-CHF-001 |
| Name | Jordan Avery (fictional) |
| Date of birth | 1958-04-03 |
| Age at encounter | 68 |
| Sex recorded at birth | Male |
| Gender identity | Not documented |
| Encounter ID | ENC-SYN-2026-11014 |
| Facility/unit | Synthetic teaching hospital, 5 West |
| Admission | 2026-11-14 18:42 UTC |
| Current reference time | 2026-11-17 07:30 UTC |
| Hospital day | 3 (local counting convention: admission day is day 1) |
| Attending service | Hospital medicine with cardiology consultation |
| Code status | Full code, confirmed 2026-11-15 09:20 UTC |

## Presenting history

Four days of increasing exertional dyspnea, orthopnea, bilateral leg swelling, and a 3.2 kg weight increase from the patient's reported home baseline. Reports missing two evening doses of furosemide during a recent pharmacy delay. No chest pain, fever, productive cough, or known sick contacts at presentation. Admitted for suspected acute decompensated HFrEF with volume overload.

## Medical history

| Condition | Details | Status / source |
|---|---|---|
| Heart failure with reduced ejection fraction | LVEF 30% on echo dated 2026-08-10; chronic NYHA class II symptoms in clinic | Active, cardiology note 2026-08-10 |
| Coronary artery disease | PCI with drug-eluting stent to RCA in 2021; no documented recent angina | Active history |
| Hypertension | Longstanding | Active |
| Chronic kidney disease | Stage 3a documented; baseline creatinine 1.3–1.5 mg/dL | Active history |
| Type 2 diabetes mellitus | Most recent A1c 7.2% on 2026-09-30 | Active |
| Atrial fibrillation | Paroxysmal; sinus rhythm on most recent outpatient ECG | Active history |
| Obstructive sleep apnea | Uses CPAP at home inconsistently | Active history |

## Allergies and reactions

| Substance | Reaction | Verification |
|---|---|---|
| Lisinopril | Persistent dry cough | Patient confirmed 2026-11-15 08:55 UTC |
| Sulfonamide antibiotics | Rash as a teenager; details uncertain | Patient report 2026-11-15 08:55 UTC |
| Other | No other known drug allergies reported | Reviewed 2026-11-15 08:55 UTC |

## Home medications on reconciliation (2026-11-14 20:05 UTC)

| Medication | Home regimen reported | Reconciliation note |
|---|---|---|
| Sacubitril/valsartan | 49/51 mg by mouth twice daily | Patient reports taking most doses |
| Carvedilol | 12.5 mg by mouth twice daily with meals | Patient reports taking |
| Spironolactone | 25 mg by mouth once daily | Patient reports taking |
| Empagliflozin | 10 mg by mouth once daily | Patient reports taking |
| Furosemide | 40 mg by mouth once daily | Patient reports missing two daily doses during pharmacy delay |
| Apixaban | 5 mg by mouth twice daily | For paroxysmal atrial fibrillation |
| Atorvastatin | 40 mg by mouth nightly | For coronary artery disease |
| Metformin ER | 500 mg by mouth twice daily with meals | Held on admission per inpatient plan |

## Current and recent medication orders

| Medication/order | Dose, route, frequency | Status | Ordered / changed | Notes |
|---|---|---|---|---|
| Furosemide | 40 mg IV every 12 hours | Discontinued | 2026-11-14 20:40; stopped 2026-11-15 08:15 | Initial inpatient regimen; replaced after limited urine response |
| Furosemide | 80 mg IV every 12 hours | Active | 2026-11-15 08:16 | Reassessment planned against urine output, symptoms, renal function, and electrolytes |
| Potassium chloride | 20 mEq by mouth once | Completed | 2026-11-15 13:10 | Replacement after potassium 3.6 mmol/L |
| Potassium chloride | 20 mEq by mouth once | Completed | 2026-11-16 14:05 | Replacement after potassium 3.7 mmol/L |
| Sacubitril/valsartan | 49/51 mg by mouth twice daily | Active | Continued 2026-11-14 22:00 | Hold parameters per order: SBP < 95 mmHg or symptomatic hypotension |
| Carvedilol | 12.5 mg by mouth twice daily with meals | Active | Continued 2026-11-14 22:00 | Hold parameters per order: HR < 55 bpm or SBP < 95 mmHg |
| Spironolactone | 25 mg by mouth once daily | Active | Continued 2026-11-14 22:00 | Monitor potassium and renal function |
| Empagliflozin | 10 mg by mouth once daily | Held | 2026-11-15 07:30 | Held while inpatient during acute illness / reduced oral intake; reassess before discharge |
| Apixaban | 5 mg by mouth twice daily | Active | Continued 2026-11-14 22:00 | No active bleeding documented |
| Atorvastatin | 40 mg by mouth nightly | Active | Continued 2026-11-14 22:00 | — |
| Metformin ER | 500 mg by mouth twice daily | Held | 2026-11-14 20:55 | Inpatient hold; glucose monitored |

## Active orders and care plan

| Order | Status | Authored | Details |
|---|---|---|---|
| Admit to hospital medicine, telemetry | Active | 2026-11-14 19:05 UTC | Acute decompensated heart failure |
| Strict intake/output | Active | 2026-11-14 20:10 UTC | Document oral and IV intake and measured urine output |
| Daily standing weight | Active | 2026-11-14 20:10 UTC | Same scale when practical; document time and method |
| 2 g sodium diet | Active | 2026-11-14 20:10 UTC | — |
| Fluid goal 1.8 L/day | Active | 2026-11-14 20:10 UTC | Total oral and IV fluids |
| Furosemide 80 mg IV q12h | Active | 2026-11-15 08:16 UTC | See medication table |
| Basic metabolic panel and magnesium | Active | 2026-11-17 05:00 UTC | Daily during IV diuresis |
| Ambulatory oxygen saturation | Active | 2026-11-17 09:00 UTC | Room air if tolerated; report symptoms and saturation |
| Repeat transthoracic echo | Completed | 2026-11-15 14:30 UTC | LVEF 30%; no new major valvular finding reported |
| Consider metolazone if inadequate response | Discussion only | Mentioned 2026-11-16 18:50 UTC | No order was placed; decision deferred pending morning reassessment |

## Vitals

| Date/time UTC | BP mmHg | HR bpm | RR/min | Temp °C | SpO₂ | O₂ | Weight kg | Source |
|---|---:|---:|---:|---:|---:|---|---:|---|
| 2026-11-14 19:05 | 146/88 | 104 | 22 | 37.1 | 92% | Room air | 92.4 | ED triage |
| 2026-11-15 06:15 | 132/78 | 88 | 20 | 36.8 | 95% | 1 L nasal cannula | 92.0 | Nursing observation |
| 2026-11-15 17:50 | 124/74 | 82 | 18 | 36.7 | 96% | 1 L nasal cannula | 91.6 | Nursing observation |
| 2026-11-16 06:05 | 118/70 | 76 | 18 | 36.6 | 95% | Room air | 90.9 | Standing scale |
| 2026-11-16 17:55 | 114/68 | 74 | 17 | 36.8 | 96% | Room air | 90.8 | Nursing observation |
| 2026-11-17 05:55 | 110/66 | 72 | 18 | 36.7 | 96% | Room air | 90.2 | Standing scale |

## Laboratory results

| Test | 2026-11-14 19:20 | 2026-11-15 05:10 | 2026-11-16 05:05 | 2026-11-17 05:00 | Units | Reference interval (illustrative local range) |
|---|---:|---:|---:|---:|---|---|
| Sodium | 137 | 138 | 139 | 139 | mmol/L | 135–145 |
| Potassium | 4.1 | 3.6 | 3.7 | 3.8 | mmol/L | 3.5–5.1 |
| Chloride | 102 | 101 | 102 | 103 | mmol/L | 98–107 |
| CO₂ / bicarbonate | 23 | 25 | 27 | 28 | mmol/L | 22–29 |
| BUN | 28 | 30 | 32 | 33 | mg/dL | 7–20 |
| Creatinine | 1.42 | 1.48 | 1.52 | 1.49 | mg/dL | 0.7–1.3 |
| eGFR (reported) | 54 | 51 | 49 | 50 | mL/min/1.73 m² | ≥60 |
| Magnesium | 1.9 | 1.8 | 1.9 | 2.0 | mg/dL | 1.7–2.4 |
| Glucose | 182 | 154 | 142 | 138 | mg/dL | 70–140 fasting |
| Hemoglobin | 12.7 | 12.3 | 12.1 | 12.2 | g/dL | 13.5–17.5 |
| WBC | 8.8 | 8.1 | 7.6 | 7.4 | ×10⁹/L | 4.0–11.0 |
| Platelets | 214 | 207 | 202 | 205 | ×10⁹/L | 150–400 |
| BNP | 1,240 | — | — | — | pg/mL | <100 (context-dependent) |
| High-sensitivity troponin | 28 | 27 | — | — | ng/L | 0–19 (assay-specific) |

## Imaging and cardiac tests

| Date/time UTC | Study | Result summary |
|---|---|---|
| 2026-11-14 20:05 | Chest radiograph | Mild bilateral interstitial prominence and small bilateral pleural effusions; no focal air-space consolidation reported. |
| 2026-11-14 21:15 | ECG | Atrial fibrillation with ventricular rate 98 bpm; no acute ST-elevation reported. |
| 2026-11-15 14:30 | Transthoracic echo | LVEF approximately 30%; moderate global hypokinesis; no new major valvular abnormality compared with prior study. |

## Intake and output

| Interval | Intake | Urine output | Net balance | Notes |
|---|---:|---:|---:|---|
| 2026-11-14 19:00–2026-11-15 06:00 | 1,300 mL | 1,050 mL | +250 mL | Initial IV furosemide dose given |
| 2026-11-15 06:00–2026-11-16 06:00 | 1,450 mL | 2,650 mL | −1,200 mL | Dose increased during interval |
| 2026-11-16 06:00–2026-11-17 06:00 | 1,520 mL | 2,280 mL | −760 mL | Nursing record complete through 06:00 |

## Source and timestamp conventions

All timestamps are UTC and are fabricated for this case. Some conversational recollections may be imprecise; structured chart values should be interpreted with their own timestamps and source attribution. A medication marked “discussion only” is not an order. Status and effective times matter when determining what is current at the 2026-11-17 07:30 reference time.

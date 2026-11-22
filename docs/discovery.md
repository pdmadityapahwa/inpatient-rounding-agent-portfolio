# Product Discovery

**Status:** Initial discovery inputs; volume and time figures are assumptions pending SME/clinician approval.

## Users and stakeholders

- **Primary users:** Hospitalists and physicians who create or review inpatient progress notes.
- **Clinical validators:** SMEs and clinicians who must review and approve the workflow, requirements, and synthetic clinical content.
- **Human approval boundary:** The system drafts a note for clinician review and signature. It does not sign or write to a real EHR.

## Workflow and feature touchpoint

Before morning rounds, the system prepares a SOAP progress-note draft for one synthetic inpatient using the available chart and prior note. The clinician reviews and signs the note. The system does not replace clinical judgment or the clinician's approval.

## User journey and milestones

1. Before morning rounds, the clinician opens the patient chart and prior progress note.
2. The system reviews the relevant chart information and prepares a source-referenced draft.
3. The clinician reviews, edits as needed, and signs the note.

The feature enters at the pre-rounds chart review and drafting milestone, and ends at clinician review/sign-off. This journey is carried forward from the project brief and remains subject to clinician validation.

## Initial workflow-volume assumptions

- **Planning assumption:** Approximately 200 progress notes are generated per day at one site.
- **Per-patient cadence assumption:** Approximately one progress note per patient per day.
- **Manual time assumption:** Approximately 15 minutes to generate one progress note.
- **Implied aggregate effort:** 200 notes/day × 15 minutes = 3,000 minutes, or about 50 staff-hours per day.

These are discovery assumptions, not measured baseline data. Validate the site scope, note volume, cadence, and time estimate with SMEs/clinicians before using them as business-case claims or KPI baselines.

## Validation needed

- Confirm whether hospitalists and physicians are one primary persona or whether distinct persona profiles are needed.
- Confirm the workflow and user journey with clinicians, including handoffs and review/sign-off behavior.
- Validate the daily volume and 15-minute estimate, and clarify whether the 200 notes/day refers to a single site.
- Obtain SME/clinician approval of the discovery findings before treating them as validated requirements.

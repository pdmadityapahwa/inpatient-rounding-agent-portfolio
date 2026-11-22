# Run predictions

## First local model run — 2026-11-21

- **User prediction:** Skipped at user's request.
- **Codex forecast recorded before run:** The retriever should return the 90.2 kg 05:55 standing weight, 05:00 labs, interval I/O, current patient-reported dyspnea, active furosemide 80 mg IV q12h, and pending 09:00 ambulatory oxygen check. It should exclude metolazone as an order, the rounded handoff weight as a measurement, and any 100 mg furosemide change. Likely risks: schema/source-ID mismatch because source references vary across markdown sections, and the full transcript may cause the 10-second deadline to expire.
- **Outcome:** First attempt ran inside the sandbox and could not reach the model API (`APIConnectionError`). A network-enabled run reached the API, which returned a billing/credits error: no credits remained. The app displayed the prior note unchanged with the failure message. No model response was produced, so this is not an agent-quality result. An initial iteration retried the same billing error three times; the retry policy now stops immediately on billing/credit and authentication errors.
- **Portfolio decision:** The PM chose to skip paid model runs. No further live inference or model-quality evaluation will be attempted; report the targets as not evaluated.

# Agent implementation notes

**Status:** Initial implementation scaffold; not evaluated and not clinically validated.

**Portfolio scope decision:** The PM chose not to pay for live model inference. No paid model run or agent-quality evaluation will be performed for this portfolio; all quality and latency targets remain unevaluated.

## Components

- `src/rounding_agents/app.py` contains the case loader, retrieval agent, documentation agent, source-reference validation, retry/fallback orchestration, note renderer, and JSONL run logger.
- Each agent makes a separate OpenAI Responses API call and returns schema-constrained JSON. The retriever receives the synthetic source packet; the documentation agent receives its evidence packet plus the prior note.
- Application retries are capped at three retries total after the initial attempt, shared across agents. Only the failing agent is retried; a successful evidence packet is retained if documentation fails. SDK retries are disabled so retries are visible in the run trace. All attempts share a 10-second wall-clock deadline; when it expires, the exact prior note text is returned with a failure message.
- Billing/credit and authentication failures are treated as non-retryable; repeating them cannot restore access and would only waste time. Temporary rate limits and transport/server failures remain eligible within the shared retry and deadline budgets.
- The prototype in `prototype/index.html` remains a separate simulated workflow artifact.

## Product assumptions and open decisions

- Current implementation uses one configured model for both agents. Per-agent model selection is deferred until quality, latency, and cost are measured.
- The full synthetic packet is sent to the retriever for this small fixture. A larger chart will require context selection or retrieval indexing and a new latency/cost evaluation.
- Structured output guarantees shape, not clinical correctness. Source checks only confirm that cited IDs appeared in the evidence packet; clinician review and fact-level evaluation remain necessary.
- The current provisional golden set is not used as approved ground truth.
- 10 seconds is enforced as an end-to-end deadline, but feasibility is unknown until a configured API run is measured. Retries may not fit in the remaining time.
- No cost-per-run value is asserted. The JSONL log records per-agent token counts and request IDs so cost can be calculated later from the applicable model rate card.
- The local fallback prints the unchanged prior note and warning; the prototype UI has not been connected to this code.

## Run locally

1. Create a virtual environment and install `requirements.txt`.
2. Copy `.env.example` to `.env` and set a development API key in `OPENAI_API_KEY`.
3. Run `python -m src.rounding_agents.app` from the repository root.

The source fixture and generated output are synthetic and not for clinical use. The implementation has not been evaluated against the project targets. A previous launch attempt reached the API but received a no-credits billing response; it produced no model output. The PM then chose to skip paid runs.

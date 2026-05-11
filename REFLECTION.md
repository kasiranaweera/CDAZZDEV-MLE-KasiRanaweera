# REFLECTION.md

## Architectural Decisions

**Task 1 — Financial AI Pipeline**

Pydantic was chosen over raw JSON validation for automatic type coercion and field-level validators
that surface exactly which field failed — critical when debugging LLM output at speed. Groq
Llama-3.3-70b-versatile was selected for sub-second inference latency (~700 tokens under 1s) and
the nuanced financial reasoning its 70B parameter count produces versus smaller models. AAPL was
chosen as the ticker for dense news coverage, well-populated yfinance data, and consistent P/E
reporting, minimising null-value pipeline breaks. Wilder's EWM smoothing (alpha=1/period,
adjust=False) was used for RSI to align with industry charting platforms for comparability.

**Task 2 — Fine-Tuning Pipeline**

Mental health triage was selected as the use case because its structured output schema is grounded
in established clinical frameworks (Columbia Protocol, PHQ-9), enabling rigorous hallucination
measurement without requiring clinical expertise. Phi-3-mini-4k-instruct (3.8B) was chosen as the
student model — it fits within Colab T4 VRAM under 4-bit quantization while its Microsoft
instruction-following training provides a meaningful baseline to improve upon. Groq Llama-3-70B
served as the teacher — a fundamentally different model, avoiding the circular training signal that
would result from using the same model for both roles. The scenario matrix approach guaranteed
diversity across 4 severity levels, 12 concern types, and varied demographics, preventing
near-duplicate homogeneity. LoRA rank=16 was chosen as the midpoint between capacity (r=32,
higher VRAM) and speed (r=8, insufficient for structured JSON adaptation), with alpha=32 following
the validated 2× scaling convention.

**Task 3 — Multi-Agent System**

Task 3A uses LangGraph's `create_react_agent` for its production-grade observe-reason-act loop,
automatic tool schema injection, and maintained message history. Task 3B switches to a manual
`_react_loop` to gain precise control over the critique loop and deterministic handoff assertion —
demonstrating when to use a framework versus owning the loop. Tool restriction is enforced
architecturally via `llm.bind_tools()`, not prompt-level instructions, so Agent B cannot call
price tools because the schema is never provided. The `DataBrief` Pydantic model acts as a typed
interface contract between agents, surfacing malformed handoffs immediately. `AgentTracer.log()`
runs synchronously inside every `@tool` function so `agent_trace.jsonl` is written incrementally —
a mid-run crash still preserves all prior calls.

---

## What I Would Improve With More Time

1. **Streaming LLM responses** — improve UX for longer analysis in Task 1 and Task 3 reports.
2. **Dataset scale (Task 2)** — 200–300 examples would reduce severity boundary confusion between high/moderate anxiety presentations.
3. **DPO stage (Task 2)** — a Direct Preference Optimization pass after SFT would improve response personalisation.
4. **LangGraph multi-agent graph (Task 3)** — replace the manual coordinator with a `StateGraph` for parallel tool execution and cleaner interrupt/resume in the critique loop.
5. **Async tool execution (Task 3)** — `asyncio.gather()` for price data, volatility, and news fetches concurrently; estimated 3× speed improvement.

---

## Limitations Encountered

- **yfinance news endpoint** — sometimes returns fewer than 10 headlines for less-covered tickers; mitigated with GNews RSS fallback (Task 1).
- **Groq rate limits** — free tier constrained generation speed across all tasks; mitigated with exponential backoff (Tasks 1, 2) and `time.sleep(2)` between agents (Task 3).
- **T4 VRAM (Task 2)** — 15 GB constrained batch size to 2; gradient accumulation simulated effective batch size of 16.
- **LLM JSON compliance (Task 3)** — LLaMA-3.3-70b occasionally wraps JSON in markdown fences; stripping triple-backtick blocks before `json.loads()` is a reliable guard.
- **SMA-200 warmup (Task 1)** — first 200 rows carry NaN SMA-200 values, expected and documented in notebook output.
# CITATIONS.md

## AI-Assisted Code

All AI assistance documented per Section 2.2 of the CDAZZDEV assessment brief.

### Task 1 — Financial AI LLM-Powered Equity Research
```
# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Write Pydantic models for LLM structured output in equity research',
# Date: 2026-05-09

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Design system and user prompts for financial sentiment analysis with Groq',
# Date: 2026-05-09

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Generate matplotlib 3-panel technical analysis chart for equity research',
# Date: 2026-05-09
```
### Task 2 — Mental Health Triage Fine-Tuning Pipeline
```
# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Generate pip install block for QLoRA fine-tuning pipeline',
# Date: 2026-05-10

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'QLoRA 4-bit NF4 config for Phi-3-mini TRL SFTTrainer',
# Date: 2026-05-10

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'BERTScore evaluation loop for structured JSON outputs',
# Date: 2026-05-10
```
### Task 3 — Multi-Agent Financial Research System
```
# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Implement five LangChain @tool wrappers for financial research:
#          get_price_data, get_news, calculate_volatility, llm_sentiment, web_search
#          with session memory writes and JSONL observability tracing',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Design a JSONL observability tracer with session_id, timestamps,
#          tool inputs, truncated outputs (≤200 chars), and wall-clock durations',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Write an observe-and-replan agent system prompt enforcing autonomous
#          tool selection with graceful error handling and a 3-section report',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Write structured financial sentiment system prompt with Pydantic
#          validation, weighted aggregate_score, and graceful fallback',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Write Agent A system prompt for quantitative equity data analysis
#          with structured JSON DataBrief output',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Write Agent B system prompt for qualitative research synthesis
#          with structured clarification_request critique loop JSON',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Build a Streamlit dashboard that reads agent_trace.jsonl and displays
#          tool call timeline, duration bar chart, pie chart, session selector,
#          and expandable detail rows with Plotly visualisations',
# Date: 2026-05-11

# AI-ASSISTED: Claude (claude-sonnet-4-6),
# Prompt: 'Implement persistent JSON cache with date-keyed detection and
#          short-term session memory demonstration without re-calling tools',
# Date: 2026-05-11
```
---

## Teacher Model Data Generation (Task 2)

- Model: Groq llama3-70b-8192
- Full system prompt: See Cell 5 (TEACHER_SYSTEM_PROMPT constant)
- Date: 2026-05-10

---

## Open-Source Libraries

### Task 1
- SOURCE: yfinance documentation — https://pypi.org/project/yfinance/
- SOURCE: Wilder RSI formula — https://school.stockcharts.com/doku.php?id=technical_indicators:relative_strength_index_rsi
- SOURCE: MACD definition — https://school.stockcharts.com/doku.php?id=technical_indicators:macd-histogram
- SOURCE: Bollinger Bands — https://www.bollingerbands.com/bollinger-bands

### Task 2
- SOURCE: TRL SFTTrainer docs — https://huggingface.co/docs/trl/sft_trainer
- SOURCE: PEFT LoraConfig — https://huggingface.co/docs/peft/conceptual_guides/lora
- SOURCE: BitsAndBytes QLoRA — https://github.com/TimDettmers/bitsandbytes

### Task 3
- LangChain / LangGraph : https://github.com/langchain-ai/langgraph        (MIT / Apache 2.0)
- LangSmith             : https://github.com/langchain-ai/langsmith-sdk    (MIT)
- yfinance              : https://github.com/ranaroussi/yfinance            (Apache 2.0)
- duckduckgo-search     : https://github.com/deedy5/duckduckgo_search      (MIT)
- Pydantic v2           : https://github.com/pydantic/pydantic              (MIT)
- Groq Python SDK       : https://github.com/groq/groq-python               (Apache 2.0)
- Streamlit             : https://github.com/streamlit/streamlit            (Apache 2.0)
- Plotly Python         : https://github.com/plotly/plotly.py               (MIT)
- pandas / numpy        : standard scientific Python stack                  (BSD)
- pyngrok               : https://github.com/alexdlaird/pyngrok             (MIT)
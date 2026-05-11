
# Page 1

Section 1 - General Instructions
1.1 Assessment Structure
This assessment comprises three independent tasks. Each task is self-contained, scored out of 100 points, 
and evaluates a distinct domain of senior-level machine learning engineering. You may complete one, two, 
or all three tasks. Completing additional tasks increases the weight of your application candidates who 
complete all three and perform well across all domains are given priority for the role.
Task
Domain
Core Deliverable
Marks
Task 1
Financial AI
LLM-powered equity research pipeline with structured outputs
100
Task 2
Generative AI
Domain-specific fine-tuning pipeline with rigorous evaluation
100
Task 3
Agentic
Workflows
Multi-agent financial research system with memory and
observability
100
1.2 Recommended Free Tools and Platforms
Purpose
Platform / Library
Access
GPU Compute
Google Colab (free T4 / L4 GPU)
Free - colab.google.com
LLM Inference API
Groq API - Llama-3, Mixtral
Free tier - console.groq.com
LLM Inference API
OpenRouter - multiple open models
Free models available - openrouter.ai
Model Hosting & Download Hugging Face Hub
Free - huggingface.co
Fine-Tuning Libraries
PEFT, TRL, BitsAndBytes, Transformers
Free - pip install
Financial Data
yfinance, Alpha Vantage (free tier)
Free - pip install yfinance
Vector Database
ChromaDB (local)
Free - pip install chromadb
Agent Framework
LangChain / LangGraph
Free - pip install langchain
Agent Framework
CrewAI (open-source)
Free - pip install crewai
Experiment Tracking
Weights & Biases (free personal tier)
Free - wandb.ai
Web Search (agent tool)
duckduckgo-search
Free - pip install duckduckgo-search
Version Control
GitHub (public repository)
Free - github.com
Section 2 - AI Tools and Citation Policy
The use of AI coding assistants and language models is fully permitted during this assessment. This 
reflects real-world engineering practice at CDAZZDEV, where engineers are expected to use the best 
available tools effectively. However, the assessment evaluates your architectural judgment and 
engineering decisions — not your ability to generate code. You will be asked to explain and defend every 
part of your submission during the follow-up interview.


# Page 2

2.1 What is Permitted
• GitHub Copilot, Cursor, Claude, ChatGPT, Gemini, or any AI assistant for code generation and 
debugging.
• LLMs used as teacher models for synthetic data generation (e.g. GPT-4o via OpenRouter free tier, Groq 
Llama-3-70B).
• AI-generated boilerplate, documentation drafts, and code comments.
• Referencing and adapting open-source repositories provided the source is cited.
2.2 Citation Requirements
For every instance of AI assistance or external code used, you must include a citation. Citations must
appear either as inline code comments or in a dedicated CITATIONS.md file in your repository root.
Submissions without citations where AI was clearly used will be penalised for academic integrity.
Required citation format:
For AI-generated code:
# AI-ASSISTED: Claude (claude.sonnet-4), Prompt: 'Write a function to compute RSI with
Wilder smoothing', Date: 2026-03-01
For adapted open-source code:
# SOURCE: Adapted from https://github.com/example/repo, file: trainer.py, Lines 45-82
For teacher-model data generation, include the full system prompt used in an appendix notebook cell or README
section.
2.3 What Disqualifies a Submission
• Hardcoded API keys, Hugging Face tokens, or any credentials committed to the repository.
• Notebook outputs cleared before submission - reviewers must see executed cell results.
• A design document or slide deck submitted in place of working, executable code.
• The repository is private or inaccessible at the time of review.
• Plagiarised submission - copying another candidate's or public solution without modification or citation.
Section 3 - Submission Requirements
All deliverables must be submitted via a reply to the assessment email. Ensure every link is publicly 
accessible before sending. Broken or private links will be treated as missing submissions.
Deliverable
Format & Access Requirements
Required
GitHub Repository
Public repository named CDAZZDEV-MLE-[YourName]. Must contain all
notebooks, scripts, and a root README.md. Organised into
task1_financial/, task2_genai/, task3_agentic/ sub-folders for each task
attempted.
Mandatory
Colab Notebook(s)
One notebook per task. Cell outputs must be visible — do not clear before
submitting. Include a Colab badge or direct link in the task sub-folder
README.
Mandatory
Hugging Face
Model (Task 2 only)
Fine-tuned model pushed to Hugging Face Hub. Repository may be 
private - if private, grant read access to the CDAZZDEV reviewer 
account specified in the email. Public repository is preferred.
Task 2
Google Drive -
Model Files (if HF 
not used)
Shareable Google Drive link with 'Anyone with link can view' permission.
Verify the link opens in an incognito window before submitting.
Task 2 alt.


# Page 3

Deliverable
Format & Access Requirements
Required
Agent Trace Log
(Task 3 only)
agent_trace.jsonl file containing every tool call, inputs, outputs, and
duration. Committed to the repository under task3_agentic/logs/.
Task 3
CITATIONS.md
Root-level file documenting all AI tool usage and any open-source code
adapted. See Section 2.2 for required format.
Mandatory
REFLECTION.md
Maximum 600 words. Cover: architectural decisions made, what you
would improve with more time, and any limitations encountered. One file
covers all tasks attempted.
Mandatory
Video Walkthrough
(Optional)
Screen recording of maximum 5 minutes demonstrating your solution.
Submitted as a Google Drive or YouTube (unlisted) link. Earns up to 5
bonus points per task if included.
Optional (+5
bonus)
Submission checklist - verify before sending your email:
• GitHub repository is public and accessible from an incognito/private browser window.
• All notebook cell outputs are visible (not cleared).
• No API keys, tokens, or credentials exist anywhere in the repository.
• Hugging Face or Google Drive model link opens without requiring a login (or access has been
granted).
• CITATIONS.md is present and complete.
• REFLECTION.md is present and within the 600-word limit.
• agent_trace.jsonl is present in the repository (Task 3 only).


# Page 4

Task 1 - Financial AI
LLM-Powered Equity Research
Assistant | 100 Points
Background and Objective
Equity research analysts invest significant time reading financial data, news, and earnings reports to form 
investment theses. This task requires you to build an automated equity research assistant that ingests real 
financial market data, applies LLM-based reasoning, and produces a structured analysis report 
replicating the first-pass analytical work of a junior analyst.
Task 1A - Financial Data Pipeline
Build a data ingestion and feature engineering module that performs the following:
• Fetches a minimum of two years of daily OHLCV (Open, High, Low, Close, Volume) data for a ticker of
your choice using yfinance.
• Computes the following technical indicators programmatically without using TA-Lib: 50-day Simple
Moving Average, 200-day Simple Moving Average, RSI with period 14, MACD with parameters (12, 26,
9), and Bollinger Bands with window 20 and 2 standard deviations.
• Retrieves a minimum of ten recent news headlines for the chosen ticker using any free source such as
the yfinance news endpoint, NewsAPI free tier, or an RSS feed.
• Produces a clean summary dictionary containing: current price, 52-week high and low, price-to-earnings
ratio where available, year-to-date return, and a momentum signal derived from your computed
indicators.
• Handles missing or null data without raising unhandled exceptions.
Criterion
Description
Marks
OHLCV Data Fetch
At least two years, correct ticker, no
hardcoded date strings
10
Indicator Accuracy
All five indicators computed correctly 
from first principles - no TA-Lib
25
News Retrieval
Ten or more headlines from a working
free source
10
Summary Dictionary
All required fields present and
correctly populated
10
Robustness
Missing data handled; no magic
numbers; code is readable and
commented
5
Task 1A Total
60
Task 1B - LLM Sentiment and Signal Reasoning
Using the pipeline output from Task 1A, integrate an LLM via a free inference API (Groq, OpenRouter, or 
equivalent) to perform the following reasoning steps:
• Pass each news headline to the LLM and return a structured JSON object per headline containing:
headline, sentiment (positive, negative, or neutral), confidence (a value between 0 and 1), and
brief_reason. Aggregate these into a single overall sentiment score.


# Page 5

• Provide the LLM with the computed technical indicators and instruct it to produce a reasoned Buy, Hold, 
or Sell signal with a justification of three to five sentences. The model must reason over the combination 
of indicators, not merely restate their individual values.
• Enforce structured output using Pydantic validation or JSON schema. All LLM responses must be 
validated before use. Validation failures must be caught, logged, and handled gracefully.
• Separate prompt logic from business logic - prompts should be defined as constants or loaded from 
template strings, not embedded inline throughout the code.
Criterion
Description
Marks
Per-Headline JSON
Correct schema with all four fields;
aggregation logic is sound
10
Signal Reasoning Quality
LLM reasons over indicator
combinations, not just echoes values
15
Structured Output Validation
Pydantic or schema validation
present; failures logged
10
Prompt Engineering
Clean prompt separation; system/user
roles correctly defined
5
Task 1B Total
40
Bonus - Report Rendering (up to 5 points):
Combine outputs from 1A and 1B to produce a one-page equity research brief in Markdown containing: company 
snapshot, technical outlook, news sentiment summary with top three headlines, LLM recommendation with 
reasoning, and a mandatory risk disclaimer. Render as a styled HTML page or PDF with at least one embedded 
matplotlib chart. Bonus marks are awarded for completeness and visual quality of the output.
Task 1 - Scoring Threshold
70 or above: Demonstrates production-level financial AI engineering. | 50 to 69: Adequate - gaps in robustness or 
prompt engineering. | Below 50: Does not meet the standard for this role.


# Page 6

Task 2 - Generative AI
Domain-Specific Fine-Tuning
Pipeline | 100 Points
Background and Objective
General-purpose language models produce inconsistent outputs on specialised domain tasks and 
frequently hallucinate domain-specific facts. This task requires you to design and execute a complete, 
production-quality fine-tuning pipeline that measurably improves a model's performance on a chosen 
domain task and then rigorously prove that the improvement is real.
Task 2A - Use Case Definition and Dataset Engineering
Select a domain-specific use case. Strong choices include but are not limited to: legal clause extraction, 
medical triage question answering, code review assistance, supply chain anomaly explanation, or 
compliance policy assistance. Generic chatbots and creative writing tasks will receive a maximum of 5 out 
of 30 marks for this section regardless of execution quality.
• Define the use case in a structured problem statement specifying: what the model receives as input,
what it must produce as output, and what constitutes a correct versus incorrect response.
• Generate a minimum of 100 training examples using a capable teacher model. Suitable free options
include Groq Llama-3-70B or GPT-4o via OpenRouter free tier. Include the full system prompt used for
data generation in your submission.
• Validate dataset diversity by reporting a distribution of prompt lengths and a keyword or topic frequency
analysis. Datasets where the majority of examples are minor variations of a single scenario will receive
zero marks for the diversity criterion.
• Format examples as JSONL using the correct chat template for your chosen base model with system,
user, and assistant turns.
• Split the dataset into training (80 percent), validation (10 percent), and test (10 percent) sets and report
the size of each.
Criterion
Description
Marks
Use Case Quality
Domain-specific, non-trivial, with clear
input/output/success criteria
10
Dataset Size
Minimum 100 examples; teacher
model prompt included
5
Dataset Diversity
Diversity metrics reported; no
homogeneous near-duplicate sets
10
Format and Split
Correct JSONL chat format; 80/10/10
split with sizes stated
5
Task 2A Total
30
Task 2B - Fine-Tuning Execution
Fine-tune a model using QLoRA (4-bit NF4 quantization) on Google Colab free tier. Any model from 
Hugging Face Hub is acceptable, for example LLaMA-2-7B, Mistral-7B, or Phi-3-mini.
• Justify every hyperparameter explicitly. Required documentation: LoRA rank (r), LoRA alpha, target
modules, learning rate, learning rate scheduler, number of epochs, batch size, gradient accumulation
steps, and maximum sequence length. Do not leave any parameter at its default without a written


# Page 7

reason.
• Log training loss and validation loss per epoch. The validation loss must decrease across epochs. Use 
Weights and Biases free tier or manual logging - include a screenshot or log output in the notebook.
• Merge the LoRA adapters into the base model using merge_and_unload() and save the merged model. 
Push to Hugging Face Hub (free) or save to Google Drive and include the link in your submission.
• If you encounter out-of-memory errors, document the error, what you attempted, and the solution 
applied. This demonstrates professional debugging practice.
Criterion
Description
Marks
QLoRA Implementation
4-bit NF4 quantization correctly
configured; PEFT applied
10
Hyperparameter Justification
All parameters documented with 
written reasoning - no unexplained 
defaults
15
Loss Monitoring
Train and val loss per epoch shown;
val loss decreases
10
Model Saved
Merged model saved and accessible
via provided link
5
Task 2B Total
40
Common errors that will lose marks:
• Training on fewer than 30 examples and claiming the model is fine-tuned.
• Using the same model as both the teacher (data generator) and the student (model being fine-tuned).
• Submitting a notebook with cleared outputs - no evidence of execution means no marks for 
execution.
• Hardcoding an API key or Hugging Face token anywhere in the submitted code.
Task 2C - Evaluation and Baseline Comparison
Demonstrate that fine-tuning produced a measurable improvement. A single inference test with a 
subjective comment that the output 'looks better' will receive zero marks for this section.
• Report ROUGE-L on the held-out test set for both the base model (with a system prompt but no
fine-tuning) and the fine-tuned model. Present results in a comparison table.
• Report at least one additional metric: BERTScore F1, or an LLM-as-judge pipeline where a capable
model scores outputs on a defined rubric and returns structured JSON.
• Manually review a minimum of ten responses from the fine-tuned model. Label each as correct, partially
correct, or hallucinated. Calculate and state the hallucination rate as a percentage.
• Write two paragraphs of qualitative analysis: the first describing where fine-tuning improved the model's
behaviour with specific examples, the second describing remaining failure modes and what additional
data or training strategy would address them.
Criterion
Description
Marks
ROUGE-L Comparison
Base vs fine-tuned on identical test
set, presented as a table
8
Additional Metric
BERTScore or LLM-as-judge with
structured output
7


# Page 8

Criterion
Description
Marks
Hallucination Rate
Minimum ten responses manually
reviewed and labelled
7
Qualitative Analysis
Specific, evidence-backed
two-paragraph analysis with next
steps
8
Task 2C Total
30
Bonus - RAG Fallback Layer (up to 5 points):
Implement a retrieval-augmented generation fallback: when the fine-tuned model's confidence falls below a defined 
threshold (measured by perplexity or LLM self-rating), retrieve relevant context from a ChromaDB vector store built 
from your training domain documents and re-query the model. Include a concrete before-and-after example in the 
notebook.
Task 2 - Scoring Threshold
70 or above: Production-ready fine-tuning practice with rigorous evaluation. | 50 to 69: Adequate execution with 
gaps in evaluation depth. | Below 50: Does not meet the standard for this role.


# Page 9

Task 3 - Agentic Workflows
Multi-Agent Financial Research
System | 100 Points
Background and Objective
Agentic AI systems represent the current frontier of applied machine learning engineering. Unlike a single 
model responding to a prompt, agent systems use reasoning loops, tool invocation, memory, and 
multi-agent coordination to complete complex multi-step tasks autonomously. This task assesses whether 
you can architect, implement, and debug a real agentic system at a production standard.
Task 3A - Tool-Using Research Agent
Using LangChain, LangGraph, or CrewAI (your choice), build a single research agent that can 
autonomously respond to the following query:
Analyse the current financial health and market sentiment of [TICKER]. Identify the top three
risks to its share price over the next 90 days and suggest one data-driven hedge strategy.
The agent must have access to the following five tools, each of which you implement:
• get_price_data(ticker, period) - wraps yfinance; returns OHLCV data with computed indicators.
• get_news(ticker, n) - retrieves recent headlines and returns a structured list.
• calculate_volatility(ticker, window) - computes annualised historical volatility.
• llm_sentiment(headlines) - calls an LLM and returns a structured sentiment score.
• web_search(query) - uses the duckduckgo-search library to retrieve analyst commentary.
Behavioural requirements for the agent:
• The agent must decide autonomously which tools to call and in what order based on what it has
observed so far. Hard-coded tool call sequences will receive partial marks for this criterion only.
• Demonstrate at least one complete cycle of: tool call, observe result, decide next action based on
observation.
• Produce a final structured report with three sections: Financial Health Summary, Top Three Risks (each
with supporting evidence), and Hedge Strategy Recommendation.
• Handle tool failures gracefully. If a tool returns an error or empty result, the agent must attempt an
alternative approach rather than stopping execution.
Criterion
Description
Marks
All Five Tools Implemented
Each tool callable and returning
correct data types
15
Autonomous Tool Selection
Agent decides order based on
observations — not a fixed sequence
10
Observe and Replan Cycle
At least one visible cycle in notebook
output trace
8
Final Report Quality
All three sections present with
specific, evidence-backed content
10
Error Handling
Graceful fallback on tool failure; no
unhandled exceptions
7


# Page 10

Criterion
Description
Marks
Task 3A Total
50
Task 3B - Multi-Agent Coordination
Extend the system to a two-agent pipeline in which each agent has a distinct, specialised role and 
restricted tool access. The agents must coordinate to produce a result neither could produce alone.
Agent
Role
Tool Access
Output
Agent A Data
Analyst
Quantitative
analysis
get_price_data,
calculate_volatility, llm_sentiment
Structured JSON data brief - no 
access to web_search
Agent B
Research
Writer
Qualitative
synthesis
web_search, get_news only
Final research report - no direct 
access to price data tools
• Agent A must pass its output to Agent B using a structured schema defined with Pydantic or a typed 
dictionary. Unstructured string passing between agents will lose marks for this criterion.
• The complete agent message trace must be visible in the notebook output what each agent said, which 
tools were called, and what data was handed off between agents.
• Implement a critique loop: Agent B may send one specific clarification request back to Agent A, Agent A 
must respond with the requested data, and Agent B must incorporate it before producing the final report. 
This loop must execute at least once and be visible in the output.
• The end-to-end pipeline must complete without any manual intervention between the initial query and 
the final report.
Criterion
Description
Marks
Distinct Roles and Tool Restriction
Agents have enforced, separate tool
access
8
Structured Handoff Schema
Pydantic or typed dict - not raw string 
passing
8
Message Trace Visible
Full trace of agent actions and
handoffs in notebook output
6
Critique Loop
At least one visible
request-response-incorporate cycle
8
End-to-End Automation
Runs to completion without manual
intervention
5
Task 3B Total
35
Task 3C - Memory and Observability
• Short-term memory: the agent must maintain context across tool calls within a single session.
Demonstrate this by asking a follow-up question that the agent answers using a previously retrieved
result without re-calling the tool.
• Persistent memory: after a session completes, save the final research brief to a JSON file keyed by
ticker symbol and date. On a subsequent run with the same ticker, the system must detect the cached
file and load it instead of re-running all tools.


# Page 11

• Observability: log every tool call, its input arguments, output (truncated to 200 characters), and
wall-clock duration to a structured file named agent_trace.jsonl. This file must be present in the
submitted repository.
Criterion
Description
Marks
Short-Term Memory
Follow-up answered from context
without re-fetching
5
Persistent Cache
JSON file saved; second run detects
and loads cached brief
5
agent_trace.jsonl
File present in repo with tool name,
inputs, output, and duration per call
5
Task 3C Total
15
Bonus - Observability Platform Integration (up to 5 points):
Integrate LangSmith free tier or an equivalent observability platform and include a screenshot of at least one 
complete agent run trace in your README. Alternatively, build a simple Streamlit dashboard (free) that reads 
agent_trace.jsonl and displays the trace visually.
Task 3 - Scoring Threshold
70 or above: Demonstrates genuine agentic engineering capability at a senior level. | 50 to 69: Adequate 
single-agent work; multi-agent coordination incomplete. | Below 50: Does not meet the standard for this role.
Ceylon Dazzling Dev Holding (Pvt.) Ltd. | Senior ML Engineer Technical Assessment | Confidential — Not for Distribution


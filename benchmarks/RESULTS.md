# Results

All measurements: MacBook Pro (Apple M4 Pro, 24 GB unified memory), macOS 26, local inference only.
Model: 27B dense open-weight model, Unsloth UD-Q3_K_XL quantization (13.1 GB file), llama.cpp server, 32k context.
Period: 21 September – 10 October 2026. Machine-readable version: [results.csv](results.csv).

**Labels**
- **MEASURED**: logged runs, replicated or n ≥ 2.
- **EXPERIMENTAL**: measured, but n is small, the result comes from replay rather than the live system, or it has not been replicated.
- **RESEARCH GOAL**: not measured; stated as a target.

## 1. Task-level before/after

Wall-clock time from the moment the request is sent to the final answer, through the real desktop app, unless noted.

| Task | Before | After | n (after) | What changed | Status |
|---|---|---|---|---|---|
| Supplier quote form on a test website (14 fields, must not submit) | 35.2–38.3 s | 2.0–2.6 s | ≥ 45 passing runs | Verified core recognizes the request and fills the form; 0 model tool calls; fields re-read from the page | MEASURED |
| VAT summary over 20 synthetic invoices, exact to the cent | 631 s, fail; then 193 s, fail | 10–14 s | 49/51 reports pass (the two failures are the earliest runs) | Model makes 1 decision; invoice reading and arithmetic by the verified core | MEASURED |
| VAT summary on real-world invoices (text, XML e-invoice, OCR) | — | ≈ 11 s | 29/30 pass | Same | MEASURED |
| File 20 invoices into a new folder and open it in Finder (working folder) | 84 s | 19.9–21.1 s | 6/6 pass, hidden judge | One model tool call; filing and on-disk verification by the core | MEASURED (before: n=1) |
| File invoices from the user's Downloads into Documents (personal folders) | 33–35 s | 26.4–27.4 s | 3 | Same, under the request-scoped access rules; 0 questions | MEASURED |
| Eight end-to-end desktop tasks (G1–G8) | — | 7/8 to 8/8 | several runs, 24–27 Sep | — | MEASURED |
| Development missions (14 tasks × 2) | — | 22/28 | 28 | — | MEASURED |
| Repeat a task Nown already solved, with a tool it wrote itself (resize a folder of images) | 376 s the first time (model writes, tests on a copy, then applies the tool) | 8 s total; tool replay 1.1–1.4 s by the core | 5 replays, 1–10 Oct | The tool is stored after verification and replayed without the model | MEASURED (before: n=1) |

## 2. Model and runtime

| Measurement | Value | Conditions | Status |
|---|---|---|---|
| Decode cost model | 98.4 ms/token + 1.36 ms per 1k tokens of context | Theil–Sen fit on 2,261 requests from 80 runs | MEASURED |
| Median decode speed | 9.82 tok/s (0–4k ctx) · 9.21 (4–8k) · 8.99 (8–16k) · 8.55 (16–24k) | same | MEASURED |
| Effective memory bandwidth during decode | ≈ 124.5 GB/s, 46 % of the 273 GB/s nominal | same | MEASURED |
| Prefill cost | ≈ 589 ms fixed + 12.6 ms/token; cold start ≈ 86 tok/s | 985 requests | MEASURED |
| Reasoning mode "low" → "none" | 22/28 → 22/28; median time −48 %; generated tokens −61 % | 14 development missions × 2 | MEASURED |
| Resumed-session time to first token with our prefix-cache package | 15.5 s → 1.1 s (other scenarios: 6.8 → 1.4 s, 6.0 → 1.1 s); +0.7–0.8 GB memory | replay of captured requests, 30/30 units | EXPERIMENTAL (not yet measured on the live agent) |
| Choice of quantization: UD-Q3_K_XL vs Q3_K_M | 3/4 vs 1/4 tasks; 9.55 vs 7.81 tok/s | blind protocol, n = 4 | EXPERIMENTAL |
| Decode target on the same laptop | 16 tok/s | — | RESEARCH GOAL |

## 3. Safety and verification

| Property | Result | Status |
|---|---|---|
| When sending a web form is requested, the system asks the user first | 26/26 runs, always exactly 1 question and 1 send | MEASURED |
| Booby-trapped web page trying to make the agent send data | 14/14 runs, 0 sends | MEASURED |
| Deletion attacks against personal folders (review suite of 20) | 17/20 succeeded before the safety work → 0/20 after | MEASURED |
| Outbound non-local network connections during local operation | 0 in 663 samples (up to 11 processes tracked) | MEASURED |
| Mutation testing of the codebase | 362/362 mutants killed; 505 + 18 tests, 0 failures (29 Sep) | MEASURED |

## 4. In active development

Computer Use on open-ended real tasks, complex multi-file coding, and decode speed are in active development. Results will be published here when they meet the MEASURED bar.

## Definitions

- **Pass**: a hidden judge (script the agent cannot see) checks the final state on disk or on the page. For the VAT summary, every total must match to the cent.
- **Time**: wall clock, request sent → final answer displayed, including model, tools and verification.
- **Question**: any confirmation the system asks the user during the task.

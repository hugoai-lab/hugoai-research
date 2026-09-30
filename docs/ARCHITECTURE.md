# Architecture (simplified)

Nown is organized so that the language model is used only for what requires judgment, and everything that can be executed deterministically is executed and verified outside the model.

```
┌──────────────────────────────── laptop (offline-capable) ────────────────────────────────┐
│                                                                                          │
│  Desktop bar ──► Core ──────────────► Harness (agent loop) ──► 27B model (local runtime)  │
│                   │  ▲                     │                                             │
│                   │  │ verified answer     │ tool calls                                   │
│                   ▼  │                     ▼                                             │
│             Verified core ◄──────── Permission layer ──► files · apps · browser · shell   │
│   (deterministic actions,            (access scoped to the                               │
│    on-disk / on-page checks)          user's own request)                                │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

## Components

- **Model.** A 27B dense open-weight model, 3-bit quantized (13.1 GB), served locally by llama.cpp. Chosen after blind comparisons against other quantizations and against smaller and mixture-of-experts models on our tasks.
- **Runtime work.** Our main runtime lever so far is avoiding re-reading context: a prefix-cache package that lets resumed sessions skip most of the prompt re-evaluation (experimental).
- **Harness.** An agent loop that gives the model tools for files, shell, code, desktop applications (Computer Use) and a browser extension.
- **Core.** Orchestrates each request. For recognized, well-defined requests it hands execution to the verified core and writes the answer itself after checking the result, so the model's work is reduced to one decision or none.
- **Verified core.** Deterministic implementations of frequent actions (reading invoices, filing, filling a known form), each followed by a verification of the resulting state.
- **Permission layer.** Grants access only to what the user's own request names, for the duration of the request. Content read from a page, a file or an e-mail can never create or widen access. Sending, paying and deleting are never done without the user having asked.

## Why this matters for efficiency

A 27B model on a laptop generates about 10 tokens per second. At that speed, every avoided tool call, every avoided re-read of the context and every step moved into the verified core is worth seconds. The largest gains we have measured (≈ ×15 on a web form, 631 s → 11 s on a VAT summary) come from the system around the model, not from the model itself.

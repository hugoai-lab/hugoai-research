# E4 — How much of first-token latency is re-reading context?

**Question.** When a conversation resumes, how much of the wait before the first token is the runtime re-reading context it has already processed?

**Setup.** Requests captured from real agent sessions, replayed against llama.cpp with and without our prefix-cache package, which lets a resumed session reuse previously computed context. 30 test units.

**Result.** Time to first token on resume: **15.5 s → 1.1 s**; other scenarios 6.8 → 1.4 s and 6.0 → 1.1 s. Memory overhead +0.7–0.8 GB. 30/30 units validated.

**Limits.** Measured in replay, not yet on the live agent; hence EXPERIMENTAL.

**Status.** EXPERIMENTAL (23 Sep 2026).

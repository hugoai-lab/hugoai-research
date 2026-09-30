# E3 — Does the reasoning mode pay for itself on agent tasks?

**Question.** On a 27B model running at ≈ 10 tokens/s, is the model's built-in reasoning ("thinking") mode worth its cost for agent tasks?

**Setup.** 14 development missions, each run twice with reasoning "low" and twice with reasoning "none"; same harness, same machine, hidden judges.

**Result.** Success 22/28 in both conditions. With reasoning off: **median task time −48 %, generated tokens −61 %**. Decision: reasoning off by default.

**Why it matters.** On local hardware, every generated token costs ≈ 0.1 s. Capability that does not change outcomes is pure latency.

**Status.** MEASURED (23 Sep 2026).

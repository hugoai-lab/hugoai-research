# E1 — Verified core for a known web task

**Question.** When the user asks to fill a known supplier's quote form with their company details (and not to send it), can a deterministic, verified core replace the model's tool calls?

**Setup.** Local test website of a fictitious building-supplies supplier; 14 form fields; company profile stored locally; the supplier's address comes only from the user's own supplier list, never from a guess. MacBook Pro M4 Pro, 24 GB.

**Before.** The 27B model opens the page and writes the 14 field values as tool-call arguments: 35–38 s (≈ 11 s to decide to navigate, ≈ 17 s to generate the fill arguments at ≈ 9 tok/s).

**After.** The core recognizes the request, opens the page, fills the fields, re-reads them from the page and writes the answer: **2.0–2.6 s, 0 model tool calls**, 14/14 fields. If the request is not recognized with certainty, the model path runs unchanged.

**Safety.** The core never clicks or types into the page and therefore cannot submit. In separate scenarios, an explicitly requested send always asked the user first (26/26), and a booby-trapped page never caused a send (14/14).

**Status.** MEASURED (≥ 45 passing runs, 29 Sep 2026).

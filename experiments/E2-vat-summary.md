# E2 — Accountant-grade VAT summary, locally

**Question.** Can a local agent turn a folder of invoices into a VAT summary that is exact to the cent?

**Setup.** 20 synthetic invoices (PDF) from fictitious suppliers, including an out-of-period invoice, a duplicate and an inconsistent total; plus a real-world set mixing text PDFs, XML e-invoices and scanned documents (OCR). Hidden judge: every total must match to the cent.

**Before.** The model read and summed invoices itself: 631 s, then 193 s, both failing the judge.

**After.** The model makes one decision (which folder, which month); invoice reading, classification and arithmetic are done by the verified core, which also writes a spreadsheet and a printable PDF and reports excluded or suspicious invoices. **10–14 s, 49/51 reports pass** (the two failures are the earliest runs). Real-world set: **29/30 pass**, typically 11 s.

**Status.** MEASURED (27–29 Sep 2026).

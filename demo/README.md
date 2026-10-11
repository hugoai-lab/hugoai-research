# Demo

**Video (2 min 41 s):** https://hugoai.fr/media/nown-demo-v14.mp4

Filmed on 10 October 2026 on a MacBook Pro (Apple M4 Pro, 24 GB), with the model running locally — no cloud inference. Test data are fictitious; every duration shown on screen is measured on the take itself. The model's thinking time is shown accelerated where labelled ("accéléré ×N"); typing and actions are shown in real time.

## Script

**Opening.** Imagine an intelligent program that lives inside your computer. It drives the whole computer from the inside. Fully local — nothing goes to the cloud. Research goal: do better than frontier cloud AI, directly on your own computer. *(Goal, not a result.)*

| # | Request typed in the Nown bar | What Nown does | Measured on this take |
|---|---|---|---|
| 1 | File the PDF invoices from *Factures-reçues* into a new folder *Factures-2026*, then open it | creates the folder, moves the 20 PDFs, opens it in Finder; the bar answers in one sentence | 20 s |
| 2 | Prepare the March VAT summary from the invoices in *Factures-2026* | reads every invoice, computes VAT to the cent in code (not guessed by the model), flags a duplicate and an anomaly, generates a PDF and opens it in Preview | 11 s — VAT invoiced €2,767.34 |
| 3 | Fill the supplier's quote request form with my company details, but do not send | fills 14 fields in the browser and stops before submitting | 2.6 s |
| 4 | Resize the images of the folder *Photos-Vacances* to 1600 px | recognises a task it already knows and replays **a tool it wrote itself** (script tested on a copy before touching real files) | tool replay 1.4 s (4 photos, 15.2 MB → 1.5 MB) |
| 5 | — | the Nown bar: always on top of every app, movable, transparency adjustable down to invisible | — |

**Closing.** It doesn't just answer — it acts. Files, applications, the web: the whole computer, with your consent. Missing a tool? It writes it itself. It codes too, from inside the computer, like a person — only faster. On an ordinary computer, without the cloud; your data stays with you.

## Honesty notes

- The opening claim "do better than frontier cloud AI" is the lab's **research goal**, not a measured result.
- "Anything that can be driven digitally becomes reachable" describes the tool-writing capability in principle; the video does not show a connected device being driven.
- A broader "whole Mac" test set (Notes, Reminders, Contacts, TextEdit…) did **not** pass its gate on 9 October 2026; fixes are in progress. See [RESULTS](../benchmarks/RESULTS.md) and [METHODOLOGY](../docs/METHODOLOGY.md).

Previous 60-second single-take demo (September 2026): https://hugoai.fr/media/nown-demo-60s.mp4

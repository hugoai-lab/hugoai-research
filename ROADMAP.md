# Research roadmap

Our ambition is to build AI more capable than today’s best systems, available locally and in the cloud, with a long-term horizon of integration into future phone and computer chips.

Nown is the current local prototype. The phases below describe a research direction, not promised delivery dates. Local and cloud development can proceed in parallel; chip integration is a longer-term ambition.

| Phase | Focus | Status |
|---|---|---|
| Now | A capable local agent on a laptop: 27B model, verified core, measured safety, office tasks | MEASURED (see results) |
| Next | Whole-system efficiency: reliable Computer Use and complex coding, faster decode on the same hardware (target 16 tok/s), fewer model calls per task | IN DEVELOPMENT |
| Then | Less memory per unit of intelligence: new weight representations, learned fast paths for routine steps, smaller models where they hold up | RESEARCH GOAL |
| Capability goal | Surpass today’s leading AI on complex tasks, with explicit comparative evaluation | RESEARCH GOAL |
| Local deployment | Extend the local prototype to ordinary computers and then phones, including offline use | RESEARCH GOAL (Mac prototype already measured) |
| Cloud deployment | Develop an online version accessible independently of the user’s device computing power | DEVELOPMENT AMBITION (no cloud results reported) |
| Long-term hardware | Pursue native integration into the chips of future phones and computers | RESEARCH HORIZON (no integration or hardware partnership claimed) |

## Evidence before claims

Current measurements concern Nown on a MacBook Pro M4 Pro with 24 GB of memory. They do not establish superiority over leading general-purpose AI systems. Cloud availability, phone execution and chip integration will each require separate engineering and validation.

We will distinguish measured results, experimental findings and research goals throughout this work. See [the methodology](docs/METHODOLOGY.md) and [current results](benchmarks/RESULTS.md).

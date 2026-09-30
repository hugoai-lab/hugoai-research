# Methodology

## Principles

1. **One target machine.** Everything is measured on a single consumer laptop (Apple M4 Pro, 24 GB). A result obtained elsewhere (cloud notebook, other hardware) is used only to explore ideas, never as evidence of performance on the target device.
2. **Whole-system, end-to-end timing.** We time a task from the request to the final verified answer, including model inference, tool execution, verification and any user question. Gains are attributed to the component that produced them (model, runtime, harness or verified core).
3. **Frozen before measured.** Every change is packaged as a patch and fingerprinted (a hash of the full code tree) before it runs. A measurement job refuses to run if the tree does not match. Results therefore refer to an exact version.
4. **Gates, not impressions.** A change is installed only after fixed gates pass:
   - task judges the agent cannot see (checking the final state on disk or on the page);
   - safety scenarios (unrequested sends, booby-trapped pages, destructive actions, network isolation);
   - regression checks against a reference time for each task;
   - mutation testing: deliberately broken variants of the code must be caught by the tests.
   Gate criteria are never relaxed to let a change through. When a gate is found to be wrong, the fix is recorded with its reason.
5. **Measurement is serialized.** Measurements run one at a time from a queue, with a load guard, so no other workload contaminates timings. Tasks that drive the screen wait until the machine is idle.
6. **Every outcome is recorded.** Inconclusive and invalid outcomes are logged like positive ones.

## Labels

- **MEASURED**: logged runs, replicated or n ≥ 2, under the conditions stated.
- **EXPERIMENTAL**: measured but preliminary: small n, replay rather than live system, or not replicated.
- **RESEARCH GOAL**: a target; not measured.

## Known limitations

- Most task sets are small and built in-house; they measure progress on concrete office and agent tasks, not general intelligence.
- Some "before" values come from a single run (marked n=1).
- Model output is stochastic; we report ranges and pass counts rather than single best runs.
- We do not claim parity with any frontier model. Comparisons with hosted models are reported only with their exact conditions.

# Validation Status and Plan

**Documentation date:** October 2026. **Maturity target:** TRL 4.

## Evidence status

The development project contains an implemented bridge, test suites, process-experiment records, and an isolated configuration-authorization study. 

| Area | Available development evidence | What it supports |
|---|---|---|
| Enforcement pipeline | Source inspection identifies capability, integrity, state-dependent safety, command-history, and dispatch stages. | The components exist in code; this is not an end-to-end effectiveness measurement. |
| Component and integration tests | Test suites cover credential checks, rejection before writes, tool integrity, state-read failures, and other integration behavior. | The tests exist. A released source version still needs an accompanying execution log. |
| Earlier closed-loop experiment | The existing summary records 20 completed defended trials and 8 completed undefended trials, with zero predefined hazard events in either arm; 12 undefended trials aborted. | This experiment does not show hazard prevention, because no completed undefended trial reached the hazard. Aborts do not count as successful defense outcomes. |
| Longer-horizon process evaluation | A revised protocol specifies verified resets, elapsed-time hazard dwell, predeclared candidate sequences, and full-horizon confirmation. | An evaluation design exists. This package does not claim a completed, audited confirmatory result under that design. |
| Configuration-authorization study | An isolated controller model and report compare simple snapshot/version checks with history-aware and dependency-derived checks. | The report finds equivalent outcomes for the simpler and the more complex checks on the fixed controller. This is preliminary model-based evidence, pending independent review; no physical dynamics were evaluated. |


## TRL 4 target

TRL 4 covers integration and laboratory validation of critical components. For software, the general framework calls for functional integration, interoperability evidence, and documented test performance. This project treats that framework as a target, not as an awarded rating. See the [Technology Readiness Level definitions](https://esto.nasa.gov/trl/).

The planned laboratory deliverable integrates the agent interface, enforcement service, Modbus adapter, controller, and process simulator. It is to include a reproducible configuration and measured outcomes.

## Evaluation design

Compare defenses with the same legitimate authority, initial conditions, observation horizon, and hazard definitions. Include an undefended arm, the existing guard, and simpler policy baselines. Describe a range whitelist as a live arm only when it mediates execution, and label offline command-admission results separately.

Record three distinct outcomes:

1. **Proposal:** whether the agent proposes the target operation.
2. **Execution:** whether a call is admitted and the controller accepts the intended write.
3. **Process consequence:** whether the predefined process predicate occurs during the observation horizon.

When evaluating hazard prevention, continue observation after a rejection. Verify starting conditions, check write responses, record missing samples, and retain every aborted trial. Sustained predicates must use measured elapsed time with declared sampling-gap rules, not a nominal sample count.

## Metrics

| Metric | Reporting requirement |
|---|---|
| Unauthorized activation or execution | Count against a policy fixed before testing. |
| Process-hazard occurrence | Report events and completed-trial denominators per arm, with uncertainty intervals. |
| Time to hazard | Report measured time and censoring at the observation limit. |
| Legitimate task completion | Measure complete workflows, not only accepted individual calls. |
| False rejection | Report rejected legitimate requests and their denominator. |
| Latency and resource cost | State measurement boundaries, workload, and hardware, and report the distribution of measurements. |
| Abort and reset failure | Report separately, including reasons and any post-command failures. |

## Required evidence for a reproducible release

- Versioned implementation, dependencies, controller program, and deployment configuration.
- Frozen protocol, policy definitions, baseline configurations, and candidate-selection rule.
- Raw decisions and process trajectories, with credentials removed.
- Analysis scripts, content hashes, and a test execution log tied to the released source.
- A documented account of which claims passed, failed, or remained unresolved.

Configured process thresholds are experimental bounds unless an equipment-specific engineering basis for them is independently established. Model conformance, authorization enforcement, and physical safety must remain separate claims.

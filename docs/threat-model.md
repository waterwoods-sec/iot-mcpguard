# Threat Model

## System and assets

The protected system consists of an MCP bridge, its authorization and safety policies, a Modbus communication path, a PLC, and the process it controls. Relevant assets include control-command integrity, configuration integrity, tool-definition integrity, process operation, and availability for legitimate tasks.

The LLM agent proposes actions. The enforcement service decides whether each proposal may reach the controller.

## Attacker capabilities

The attacker may influence content that the agent reads, such as retrieved documents, operational messages, tool results, or tool descriptions. Through that content, the attacker may try to induce tool substitutions, calls to unauthorized destinations, out-of-policy parameter values, repeated commands, or sequences of individually admissible operations. Evaluation should include an adaptive attacker that can observe rejections and propose another action.

Tool-definition tampering is defined relative to the trusted manifest. A matching definition hash does not make a compromised tool implementation trustworthy, because the implementation can misrepresent its own behavior.

Under this model, the attacker does not possess the guard's signing secrets and cannot modify the trusted PLC program, forge trusted process measurements, or obtain an unmediated connection to an actuator.

## Trusted components and assumptions

| Component or condition | Assumption |
|---|---|
| Guard host and policy configuration | The attacker cannot modify the enforcement code, policy, or protected secrets. |
| Tool manifest provisioning | The initial manifest and its verification key are supplied through a trusted administrative path. |
| PLC and process-state path | The controller and direct measurement path provide authentic values within the stated experimental conditions. |
| Command mediation | Protected agent commands must traverse the guard; network or device controls prevent a direct bypass. |
| Register mapping and controller semantics | The evaluated mapping and PLC program match the running controller version. |
| Recovery and protective functions | Plant-specific protective functions remain authoritative and must be evaluated separately. |

Authentic measurements may still be stale or mutually inconsistent. Any claim that depends on measurement age, read duration, concurrent writes, or the interval before execution must record or bound those quantities.

## Protection goals

1. Reject invocations that lack valid authority for the requested tool, server, target, or operation.
2. Reject tool definitions that fail the configured integrity policy.
3. Prevent dispatched commands from violating the implemented range, state, and history policies under the declared assumptions.
4. Preserve a record of decisions, execution outcomes, and failure reasons.
5. Evaluate whether enforcement prevents predefined process hazards while allowing legitimate workflows.

Goal 5 requires closed-loop evidence, and meeting Goals 1–4 does not imply it. A command may be authorized and physically safe yet still fail to match the operator's intended task; the existing capabilities do not guarantee task-intent fidelity in general.

## Configuration-lifecycle research question

An additional policy may distinguish temporary task configuration from persistent operator-approved configuration. Under that policy, a mode change should not reactivate an expired temporary configuration without valid re-endorsement. The question concerns authorization at activation time, not retroactive cancellation of every previously authorized write.

The same scope and persistence rules must apply to every defense in a comparison. A new authorized task must still be able to adopt existing settings legitimately.

## Limits

This documentation does not claim protection against a compromised PLC, guard administrator, operating system, or trusted measurement path. It also makes no claim of general multi-server isolation, control-loop stability, continued safe operation after gateway failure, or certification for operational deployment. Physical effects already in progress may require a recovery action even after new commands are blocked.

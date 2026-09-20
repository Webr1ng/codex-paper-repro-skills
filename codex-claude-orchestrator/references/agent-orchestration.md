# Agent orchestration

Codex owns paper interpretation, architecture, data/label protocol, metrics, experiment design, conclusions, and acceptance. An execution agent may implement a specified interface, run specified commands, collect logs, or format outputs after inputs, outputs, allowed files, forbidden files, stop conditions, and checks are explicit.

```text
L0  read-only inspection or one deterministic command
L1  specified implementation or repeatable formatting
L2  bounded debugging with known interfaces and explicit checks
L3  architecture, protocol, or multi-variable experiment decision
L4  scientific conclusion, irreversible, or high-risk decision
```

L0/L1 can usually be delegated; L2 requires active review; L3/L4 remain with Codex.

## Task contract

Create `.orchestrator/tasks/TASK-<id>.md` containing level, one observable goal, minimal context, allowed changes, forbidden changes, inputs/outputs, constraints, acceptance checks, stop conditions, and a final report schema. The report must contain `status` (`SUCCESS`, `PARTIAL`, `BLOCKED`, or `FAILED`), `changed_files`, `commands_run`, `tests`, `outputs`, `git_diff_summary`, `deviations`, `unresolved`, and `acceptance_check`. Never put secrets in the contract; reference a named server profile.

## Execute and observe

Inspect an installed external CLI with `--version` and `--help` before using version-sensitive flags. Prefer non-interactive execution with bounded turns/timeouts and minimum permissions. Store raw structured output separately from human-readable diagnostics; `2>&1 | tee file.jsonl` may not produce valid JSONL. Require short observable updates: current action, command, changed files, and verification result. Do not request or rely on private chain-of-thought.

Stop the execution agent on protected-directory access, destructive commands, protocol/model changes, repeated command failure, fabricated paths, unrelated file creation, or a changed objective.

## Acceptance and recovery

After completion, independently inspect:

```bash
git status --short
git diff --stat
git diff -- <allowed paths>
```

Rerun the key test or inspect durable outputs and logs. Check interfaces, dimensions, leakage, silent fallbacks, hard-coded results/secrets, dependency scope, and evidence for every acceptance item. A “done” message or zero exit code is insufficient.

Never delegate without explicit authorization to delete data/files, overwrite checkpoints/results, modify the official repository, change CUDA/PyTorch or system packages, kill unrelated processes, change the protocol/model, force-push, or publish external artifacts.

Allow at most two attempts for the same class of error. Then preserve the log and return the failing command, error, attempted fixes, current files, and the smallest decision needed from Codex. Do not escalate through arbitrary package swaps, interpreter changes, CUDA changes, or broad cleanup.

For multi-task projects, maintain `.orchestrator/STATE.md` with goal, phase, active task, last completed task, profile, branch, important paths, known issues, pending Codex decisions, and next executable task. The execution agent may report task state but does not redefine the research goal.

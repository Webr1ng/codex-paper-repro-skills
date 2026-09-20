---
name: codex-claude-orchestrator
description: "Coordinate Codex planning and review with Claude Code or another execution agent through bounded task contracts, minimum permissions, observable logs, stop conditions, failure recovery, and independent acceptance. Use for delegated implementation, Git/SSH execution, environment operations, or report/PPT production. Do not use for autonomous research decisions or unrestricted operations."
metadata:
  short-description: "Bounded Codex and Claude Code delegation"
---

# Codex-Claude orchestrator

Use this skill for the execution boundary: decide what can be delegated, write a task contract, grant only the needed permissions, observe execution, stop on drift or risk, and independently accept the result.

Read [references/agent-orchestration.md](references/agent-orchestration.md) for task levels, contract fields, execution monitoring, acceptance, recovery, and state management. Read [references/review-notes.md](references/review-notes.md) for the security and scope changes made to the original workflow.

Codex retains paper interpretation, architecture, experiment protocol, metrics, conclusions, and final acceptance. Never place credentials in task files, prompts, logs, or reports. Do not delegate destructive, protocol-changing, or system-wide actions without explicit authorization.

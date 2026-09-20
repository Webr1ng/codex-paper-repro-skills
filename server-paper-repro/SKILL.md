---
name: server-paper-repro
description: "Run reproducible research-paper experiments on local or remote compute with checked server profiles, staged validation, durable result records, and bounded scientific conclusions. Use for paper reproduction, GPU/server experiments, and their evidence-based reports. Do not use for generic coding or unrestricted server administration."
metadata:
  short-description: "Server-based paper reproduction workflow"
---

# Server paper reproduction

Use this skill for the experimental workflow itself: server selection, environment checks, paper/code alignment, smoke tests, pilots, ablations, baselines, final validation, metrics, results, and reports.

Read [references/reproduction-workflow.md](references/reproduction-workflow.md) for the staged procedure and schemas. Read [references/review-notes.md](references/review-notes.md) when reviewing the security and consistency changes made to the original workflow.

Keep the official repository read-only by default, record the repository commit/checkpoint/dataset/environment/network mode, preserve failed and negative results, and never put credentials in skill files, prompts, logs, or reports. Conclusions must be bounded by the data, labels, preprocessing, checkpoint, threshold, and validation protocol actually used.

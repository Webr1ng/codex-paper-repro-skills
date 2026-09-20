# Reproduction workflow

Before non-trivial work, record paper, official repository and commit, checkpoint path/hash/variant, dataset name/version/split, `server_profile`, `PROJECT_ROOT`, `ENV_PYTHON`, `network_mode`, and seed. Keep credentials outside this record; a profile is a named local connection method, not a password copied into a prompt.

Recommended layout:

```text
<PROJECT_ROOT>/
├── official_repo/       # immutable by default
├── checkpoints/         # never overwrite without authorization
├── configs/             # protocol, commands, status, patches
├── data/                # raw data; do not mutate
├── logs/
├── results/{smoke_test,pilot,ablation,baseline,final_validation}/
└── scripts/             # adapters and runners
```

## Read-only checks

Honor an explicitly selected server. Otherwise inspect candidate hosts and choose based on GPU, disk, path, Python compatibility, and network access. Record the choice.

```bash
cd <PROJECT_ROOT>
pwd
<ENV_PYTHON> --version
nvidia-smi --query-gpu=index,name,memory.used,memory.total --format=csv,noheader
df -h .
ls -ld official_repo checkpoints configs data logs results scripts
curl -4 -sSIL --connect-timeout 5 --max-time 15 https://pypi.org/simple/ -o /dev/null
```

Use an existing compatible environment where possible. If isolation is needed, create a project-local `.venv` and record its interpreter. Do not change system CUDA, global Python, or another user's environment as a troubleshooting shortcut. If an approved reverse proxy or offline wheelhouse is used, record it as a network mode and whether the tunnel remains required; it does not give the remote host independent public egress.

## Staged protocol

**Phase 0: paper/code alignment.** Read paper, README, entry points, data interface, evaluation code, and checkpoint metadata. Write `configs/repro_status.md` with claimed result, implementation coverage, missing assets, mismatches, and the minimal executable command.

**Phase 1: smoke.** Use the smallest real input. Verify data loading, checkpoint loading, output shape/type, device use, and durable JSON under `results/smoke_test/`. A smoke pass only permits a pilot.

**Phase 2: pilot.** Use a small representative sample with the paper's labels, preprocessing, checkpoint, and metric. Do not tune opportunistically. Save raw scores, labels, metadata, and a summary under `results/pilot/`.

**Phase 3: diagnosis, ablation, baseline.** When a pilot is unexpected, change one variable at a time and name the hypothesis. Add at least one simple baseline on the same data and labels. Stop expanding when the failure is explained or the predeclared criterion is not met.

**Phase 4: final validation.** Before scale-up, write sample/unit split, grouping, seeds, primary/secondary metrics, threshold source, aggregation level, stop rule, and output paths. Produce `final_summary.json`, a table, figures, and limitations under `results/final_validation/`.

## Reproducibility and reporting

Each summary should include experiment name, repo commit, checkpoint hash/variant, dataset version/split/IDs, server profile, project root, interpreter, network mode, input shape, sampling rate, labels, preprocessing, model inputs, seed, device, metrics, threshold analysis, limitations, command file, and log files. Distinguish point/window/event/segment metrics; ROC-AUC is ranking evidence, while PR-AUC and fixed-threshold FP/FN answer different questions.

Figures must identify axes/units, series, checkpoint, preprocessing, displayed extent, labels versus scores, and limitations. Reports state the conclusion first, preserve negative results, and distinguish code reproducibility, checkpoint inference, pilot behavior, benchmark performance, and clinical/production claims.

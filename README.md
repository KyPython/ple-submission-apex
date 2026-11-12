# PLE Apex Self-Verifying Harness (`kyjahn-opus55-apex`)

An autonomous physical engineering agent harness for **Physical-Engineering's Last Exam (PLE)**, built for the Google-sponsored `google-cloud/claude-opus-5-5` frontier model.

## Key Innovation: 3-Phase Deliverable-Guaranteed Loop

Single-agent loops frequently compute engineering solutions correctly in reasoning while forgetting to write binary deliverable files (such as `output/submission.zip`), resulting in 0.0 scores despite correct math.

This harness implements a strict 3-phase multi-agent workflow:
1. **Planner Role (10% time budget):** Inspects the container, extracts all deliverable paths, file formats, engineering formulas, and bash verification commands without touching files.
2. **Worker Role (70% time budget):** Executes calculations via container Python scripts, implements solutions, and writes all required deliverables early.
3. **Verifier Role (20% time budget, up to 2 fix rounds):** Operates in a fresh context with container inspection tools (`bash`, `read_file`). Validates that every deliverable file exists, is non-empty (`test -s`), and that ZIP archives test clean (`unzip -t`). If any deliverable is missing, it returns a targeted fix list back to the worker before session termination.

## Files

| File | Purpose |
|---|---|
| `submission.yaml` | Declares entry name (`kyjahn-opus55-apex`), model (`google-cloud/claude-opus-5-5`), install and serve commands |
| `serve.py` | 3-phase agent loop (Planner, Worker, Verifier) over WebSocket |
| `taskbridge.py` | Competition protocol implementation and container relay |
| `requirements.txt` | Python dependencies (`openai>=1.50.0`, `websockets>=12.0`) |
| `AGENTS.md` | Operating rules for AI coding agents |

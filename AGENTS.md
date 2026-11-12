# AGENTS.md — Guidelines for `kyjahn-opus55-apex`

## Harness Protocol & Constraints
- Language: Pure Python 3.12 (managed via `uv`).
- Zero Node/NPM dependencies in runtime bundle.
- Model: `google-cloud/claude-opus-5-5` (zero cost on competition server).
- Network: Serve container has egress only to the model endpoint. Task container has no network.
- All file I/O, bash, and MCP tools must route through `taskbridge.py`.
- Preserve the 3-phase Plan $\to$ Work $\to$ Verify cycle.

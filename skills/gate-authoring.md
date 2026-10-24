---
id: gate-authoring
name: Gate Authoring
description: Write acceptance gates the barkcli runner can trust
triggers: [gate, acceptance, test-cmd, runner]
---
# Gate Authoring

The runner merges only when the acceptance gate passes **in the worktree**.
Write gates that catch the real failure modes:

1. **Fast and total.** The gate must exercise every change the task touches.
   `cargo test --quiet`, `npm test --silent`, `python3 -m pytest -q`,
   `go test ./...` — detected automatically from repo markers, or pass
   `--test-cmd "..."` explicitly.
2. **No-op gates don't count.** If the agent produces no changes, the gate
   result is rejected regardless of pass/fail. Never write a gate that passes
   vacuously (e.g. `exit 0`).
3. **Bound the flake.** If a test is flaky, fix it before enabling the pool —
   retries burn the task's `--max-attempts` budget on noise.
4. **Fail loudly.** Gate output's last 40 lines become the verdict injected
   into the retry prompt; make the first failure line name the broken thing.

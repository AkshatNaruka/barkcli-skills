---
id: flaky-test-triage
name: Flaky Test Triage
description: Diagnose and repair intermittently failing tests
triggers: [flaky, intermittent, rerun, retry]
---
# Flaky Test Triage

Before quarantine, find the root cause:

1. **Reproduce serially.** `npm test -- --runInBand` / `cargo test <name> --
   --test-threads=1`. If serial passes but parallel fails → shared state.
2. **Time travel.** Replace `sleep()`-based polling with condition polling
   (`awaitPoll(processed == N)`), or inject a fake clock.
3. **Order dependence.** Run the suite twice — once in normal order, once
   shuffled. Only the overlapping failures share causes; the singletons are
   order leaks.
4. **Resources.** Port collisions and leaked file descriptors produce
   cascading "connection refused" noise — bind ephemeral ports in tests.
5. **Decide.** Fix > quarantine > delete. Never allow-list in a way that
   hides a real regression.

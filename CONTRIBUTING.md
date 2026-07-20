# Contributing to Janus

Three things you need to know before contributing: how to verify your changes, what format to use, and where the hard boundaries are.

---

## Running Tests

```bash
# Unit tests — no API key needed (uses mocks)
pytest tests/ -v

# Individual test files
pytest tests/test_reviewer.py -v
pytest tests/test_planner.py -v
pytest tests/test_protocol.py -v
pytest tests/test_task_manager.py -v

# Integration tests — requires DEEPSEEK_API_KEY in .env
pytest tests/test_integration.py -v
```

Unit tests verify protocol correctness, reviewer verdict logic, planner dispatch, and task manager behavior — all mocked, no network calls. Integration tests exercise the full Gatekeeper → Planner → Worker pipeline with real LLM calls.

If you add a new test file, follow the existing pattern:

```python
import sys
import os
sys.path.insert(0, os.path.dirname(os.path.dirname(os.path.abspath(__file__))))

import unittest
from core.whatever import ThingYouTest
```

---

## Commits and PRs

- **Branch naming:** `feature/what-you-did` or `fix/what-you-fixed`
- **Commit messages:** One-line summary in imperative mood (e.g. `Add retry counter to TaskResult`). If it needs explanation, put it in a blank-line-separated body.
- **PR description:** State what changed and why. Link to any related issues. If your change touches a design boundary (see below), explain why it's safe.
- **Single concern per PR.** If you find an unrelated thing that needs fixing, open a separate PR.

---

## Design Red Lines

Janus is built on hard architectural boundaries. Breaking these defeats the point of the framework.

### Tools

| Role | Has tools? | Can it... |
|------|-----------|-----------|
| **Gatekeeper** | ZERO | Cannot read/write files, run commands, search the web. Pure reasoning. |
| **Planner** | ZERO | Cannot read/write files, run commands, search the web. Plans and dispatches only. |
| **Reviewer** | ZERO | Cannot read/write files, run commands, search the web. Audits via LLM reasoning on provided text. |
| **Worker** | YES | Has terminal, file read/write, web search, browser. Self-decomposes via NEEDS_DECOMPOSITION. |

Never give tools to Gatekeeper, Planner, or Reviewer. If you think a role needs one, you're solving the wrong problem — restructure the task decomposition instead.

### Context Discipline

Each role sees only what it needs:

- **Gatekeeper:** Directive (input) → ExecutionReport (output). Never sees Worker tool-call logs or Reviewer raw reasoning.
- **Planner:** Directive + historical patterns. Dispatches Workers, receives TaskResults + ReviewResults.
- **Worker:** TaskSpec only. Does not see the full conversation history, other Workers' results, or strategic intent beyond what's in `TaskSpec.intent`.
- **Reviewer:** TaskSpec + TaskResult. Does not see strategic intent or Planner dispatch logic.

If you need to pass information between roles, ask: does this role *genuinely need* this to do its job, or are you just making it convenient? Add it to the protocol dataclass (`core/protocol.py`) if the former.

### Protocol Changes

The core protocol (`core/protocol.py`) defines the data structures that flow between roles. Changes here affect every component.

- Adding a field to an existing dataclass: generally fine if `field(default=...)` preserves backward compatibility
- Removing or renaming a field: requires updating all consumers (Gatekeeper, Planner, Worker, Reviewer)
- Adding a new dataclass: explain in the PR what problem it solves and which roles produce/consume it

---

## What Needs Tests

- Any new protocol field: add a test in `tests/test_protocol.py`
- Any change to reviewer verdict logic: add a test in `tests/test_reviewer.py`
- Any change to planner dispatch or task tracking: add a test in `tests/test_planner.py`
- Any new Worker capability: add an integration test showing it works end-to-end

---

## Getting Help

Before opening a PR with a design question, read `docs/design-philosophy.md` to understand why Janus makes the choices it makes. If you're still unsure, open a discussion or issue — better to align on design before writing code.

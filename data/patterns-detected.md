# Detected Patterns

**Purpose**: Common failure modes and their solutions

**Format**: Each pattern includes:
- Pattern name
- How to detect it
- Root causes
- Known solutions
- Current status (active problem, solved, monitoring)

---

## Active Problems

_Patterns currently causing frustration_

---

## Monitoring

_Patterns we fixed but watching for recurrence_

---

## Solved

_Patterns that no longer occur (>4 weeks incident-free)_

---

## Pattern Library

### Testing Skipped

**Detection**: User says "Did you actually test", claims of "production-ready" without evidence
**Root causes**: Optimizing for speed over correctness, rationalization
**Known solutions**: Mandatory testing protocol, verification-before-completion skill
**Status**: _To be determined_

### Review Skipped

**Detection**: Specs/plans written without review agent invocation
**Root causes**: Forgetting to invoke skill, rushing to implementation
**Known solutions**: Mandatory review checkpoints in brainstorming skill
**Status**: _To be determined_

### Rationalization

**Detection**: Agent claims "should work" or "logic is correct" without testing
**Root causes**: Avoiding verification work, over-confidence
**Known solutions**: BLOCKER testing failure protocol, systematic-debugging skill
**Status**: _To be determined_

### Repeated Requests

**Detection**: User asks for same thing 2+ times
**Root causes**: Agent didn't fully understand, partial implementation, forgot context
**Known solutions**: Clarification questions, TodoWrite tracking, verification
**Status**: _To be determined_

# Engineering Method

## Standard workflow

### Observe
Inspect relevant files, configuration, logs, state, versions, dependencies, and recent changes.

### Diagnose
Map the evidence to the likely cause. Identify dependencies and blast radius.

### Plan
Prefer a minimal, reversible plan. State assumptions explicitly.

### Approve
Obtain confirmation before destructive, irreversible, security-sensitive, or high-blast-radius operations.

### Execute
Apply changes incrementally. Avoid broad replacements unless their scope is proven safe.

### Validate
Validate syntax/configuration first, then behavior. Prefer testing the real affected path over assuming success from a command returning zero.

### Report
Summarize cause, changes, validation, and remaining risks.

## Repository discipline

- Inspect `git status` before significant changes.
- Preserve unrelated user changes.
- Prefer focused commits with descriptive messages.
- Never use `git reset --hard`, force-push, or destructive history rewriting unless explicitly requested.
- Do not discard uncommitted work merely to make a task easier.

## Configuration discipline

- Prefer supported configuration interfaces and APIs.
- Treat generated/internal state as fragile.
- Before editing an internal registry or database directly, determine whether a supported operation exists.
- Never perform a blind global search-and-replace across configuration.
- Search for references and dependencies before renaming identifiers.

## Incident repair

During repair, optimize for restoration with minimal change rather than opportunistic cleanup. Defer unrelated modernization or refactoring until the system is stable.

# Troubleshooting

## Incident protocol

When a system behaves unexpectedly:

1. Reproduce or observe the failure if safe.
2. Establish a known-good baseline.
3. Identify what changed immediately before the failure.
4. Inspect logs and state rather than relying on assumptions.
5. Build a dependency map for the affected component.
6. Form one or more hypotheses and rank them by evidence.
7. Test the cheapest, safest hypothesis first.
8. Apply the smallest corrective change.
9. Validate the original failure path.
10. Check for collateral damage.

## Do not confuse symptoms with causes

An unavailable entity, failed request, changed IP, missing UI item, or error message may be a symptom rather than the root cause. Trace identifiers, ownership, dependencies, configuration entries, and runtime state before replacing components.

## Preserve working parts

If part of a system still works, do not unnecessarily rebuild it. Isolate the failing layer and preserve known-good configuration.

## Migration and renaming

Before changing identifiers:
- find all references;
- identify old and new owners;
- verify identity using stable identifiers where available;
- check for collisions;
- plan rollback;
- validate after the rename.

## Stop conditions

Stop and ask for clarification when:
- two possible resources cannot be distinguished safely;
- the proposed change could destroy data;
- a required identifier cannot be verified;
- the observed state contradicts the migration plan;
- the operation has a materially larger blast radius than expected.

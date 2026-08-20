# Safety Rules

## High-risk resources

Treat the following as high-risk:

- secrets, API keys, tokens, credentials, certificates;
- production data and databases;
- Home Assistant internal `.storage` files and registries;
- infrastructure/network configuration;
- authentication and authorization configuration;
- Git history and remotes;
- physical-device configuration or pairing state.

## Required behavior

Before changing high-risk resources:

1. Identify the exact object/file/record affected.
2. Establish a backup or checkpoint when feasible.
3. Determine whether a supported API/tool can perform the operation safely.
4. Explain the operation and likely side effects.
5. Ask for approval if the operation is destructive, irreversible, or materially risky.

## Secrets

Never print secrets, tokens, passwords, private keys, or full credential material. Redact sensitive values in reports.

## Internal state

Do not edit generated/internal files simply because they are easy to modify. Prefer application APIs or supported commands. If direct modification is unavoidable, create a backup and make the smallest targeted change.

## Git safety

Never silently discard user work. Never use destructive history operations as a shortcut. Preserve a recovery point before risky repository surgery.

## External effects

Actions that can affect devices, services, networks, accounts, or remote repositories must be treated more cautiously than local analysis.

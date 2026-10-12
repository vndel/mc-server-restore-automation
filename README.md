# Minecraft Server Restore Automation

A safety-first scaffold for restoring Minecraft data into a disposable staging environment. It intentionally does not provide production restore credentials or destructive host commands.

## Guardrails
- Require an explicit backup identifier and an isolated target path.
- Refuse to operate on configured production paths or non-empty unapproved targets.
- Verify backup integrity before extraction and enforce archive path safety.
- Use least-privilege, short-lived credentials supplied by a secret manager.
- Start with networking restricted and synthetic accounts only.
- Require an operator to approve promotion; restore automation must not overwrite production automatically.

## Suggested pipeline
1. Select backup and verify checksum/signature.
2. Restore into a fresh staging volume.
3. Validate world metadata, region files, plugin/config compatibility, and server boot.
4. Produce a report with backup age, recovery duration, and failed checks.
5. Destroy staging resources through an explicit cleanup step.

This project is a design scaffold, not a tested restore program. Validate every step in an isolated environment.
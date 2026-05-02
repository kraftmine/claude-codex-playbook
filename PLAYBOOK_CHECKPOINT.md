# Playbook: Checkpoint

Use before risky operations:

- redesign
- mass refactor
- dependency upgrade
- schema/data migration
- auth/finance/stock changes
- live deploy with meaningful behavior change

## Steps

1. Inspect state

```bash
git status --short
git diff --stat
```

2. Identify unrelated dirty work

Do not revert unrelated user/agent changes.

3. Create a local checkpoint if risk is high

Preferred:

- commit intentional work if appropriate
- or create a filesystem backup under `backups/<timestamp>-<reason>/`

4. If production is affected, create server backup before deploy

Example:

```bash
mkdir -p /var/www/<app>-backups/<timestamp>
cp -a /var/www/<app>/. /var/www/<app>-backups/<timestamp>/
```

5. Write restore notes when rollback is not obvious

Minimum restore note:

- what was backed up
- where it lives
- how to restore
- what data/schema was not included

## Output To User

Keep it short:

- checkpoint created or not needed
- backup path
- current risk
- next step

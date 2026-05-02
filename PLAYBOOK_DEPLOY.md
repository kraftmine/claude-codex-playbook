# Playbook: Deploy

Use for any live deploy.

## Pre-Deploy

1. Check worktree:

```bash
git status --short
```

2. Run tests:

```bash
npm test
```

If tests are not applicable, explain why.

3. Build:

```bash
npm run build
```

4. Smoke check the changed flow locally or in preview.

For UI changes, use a browser smoke test when possible.

5. Create server backup.

Record the backup path.

## Deploy

Use the project's known deploy command.

For Wild Kamchatka today:

```bash
rsync -av --delete dist/ root@165.22.105.41:/var/www/wild-kamchatka/
```

## Post-Deploy

1. Confirm live HTML references the new bundle.

2. Confirm the bundle URL returns HTTP 200.

3. If possible, smoke check live or state exactly what the user should test.

## Final Report

Include:

- deployed: yes/no
- live bundle
- backup path
- tests/build result
- smoke result
- what the user should manually verify

Do not make the user infer whether deploy happened.

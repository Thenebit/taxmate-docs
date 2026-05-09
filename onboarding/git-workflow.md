# Git Workflow — TaxSmart GH

## Branches

### Permanent
- `main` — production. Protected. No direct pushes.
- `develop` — integration/staging. Protected. No direct pushes.

### Temporary
- `feature/xxx` — new work
- `hotfix/xxx` — urgent production fixes
- `release/vX.X.X` — release prep

## Branch Naming

Use lowercase, hyphens, keep it short

## Daily Workflow

```bash
# 1. Start from latest develop
git checkout develop
git pull origin develop

# 2. Create your feature branch
git checkout -b feature/your-task-name

# 3. Work and commit often
git add .
git commit -m "add transaction model and schemas"

# 4. Push and open a PR into develop
git push origin feature/your-task-name
# → Open PR: feature/your-task-name → develop
```

## PR Rules

- Every change goes through a PR. No exceptions.
- At least 1 teammate must review and approve.
- All tests must pass before merge.
- Delete the feature branch after merge.

## Commit Messages

Keep them short and clear.

## Releases

```bash
# 1. Branch from develop
git checkout develop
git checkout -b release/v1.0.0

# 2. Final testing, bug fixes only

# 3. PR into main → merge → tag
git tag v1.0.0

# 4. PR release branch back into develop
```

## Hotfixes

```bash
# 1. Branch from main
git checkout main
git checkout -b hotfix/fix-vat-calculation

# 2. Fix, push, PR into main

# 3. Also PR into develop so the fix carries forward
```

## Repo Access

| Repo | Who |
|------|-----|
| `taxsmart-backend` | Backend team |
| `taxsmart-frontend` | Frontend team |
| `taxsmart-ml` | ML engineer |
| `taxsmart-docs` | Everyone (cross-team PRs for contract changes) |

## Golden Rules

1. Never push directly to `main` or `develop`.
2. One feature per branch.
3. Keep PRs small — easier to review, faster to merge.
4. Pull `develop` before creating a new branch.
5. If in doubt, ask before merging.

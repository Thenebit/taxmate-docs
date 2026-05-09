# TaxSmart GH — Documentation

Central documentation for the TaxSmart GH platform. This is the single source of truth for architecture, API contracts, and team onboarding.

## Repos

| Repo | Purpose | Team |
|------|---------|------|
| [taxsmart-backend](https://github.com/thexistech/taxsmart-backend) | FastAPI API | Backend |
| [taxsmart-frontend](https://github.com/thexistech/taxsmart-frontend) | React SPA | Frontend |
| [taxsmart-ml](https://github.com/thexistech/taxsmart-ml) | ML models & pipelines | ML |
| [taxsmart-docs](https://github.com/thexistech/taxsmart-docs) | This repo | Everyone |

## What's In Here
├── architecture/       # System design & technical decisions
├── api-contracts/      # Endpoint specs (frontend ↔ backend handshake)
└── onboarding/         # Setup guides & git workflow
More to be added.

## Quick Links

- [Git Workflow](onboarding/git-workflow.md)
- [Backend Setup](onboarding/backend-setup.md)
- [Frontend Setup](onboarding/frontend-setup.md)

## How To Use This Repo

**Starting a new feature?** Check `api-contracts/` for the endpoint spec before writing code.

**Joining the team?** Start with `onboarding/` for setup and workflow.

**Need to change an API contract?** Open a PR in this repo. Tag the relevant backend or frontend dev for review.

## Rules

1. No endpoint gets built without a contract in `api-contracts/` first.
2. Contract changes go through PRs.
3. Keep docs short and current. Delete what's outdated.

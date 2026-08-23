
# Git Branching and Promotion Workflow

1. Creating DEV/QA/PPD/PROD from a production baseline.
2. Multiple developers working simultaneously.
3. Multiple feature branches.
4. Feature branches becoming outdated while development continues.
5. Updating a feature branch from DEV.
6. Pull requests and code review.
7. DEV integration.
8. DEV → QA promotion.
9. QA finding a bug.
10. Creating a bugfix from the correct branch.
11. Re-promoting a fix to QA.
12. QA → PPD promotion.
13. PPD validation.
14. PPD → PROD.
15. Production tagging/versioning.
16. New development continuing after a release.

17. ===============================

# Git Branching Strategy

## Four Long-Lived Branches

- `dev`
- `qa`
- `ppd`
- `prod`

## Short-Lived Working Branches

### Feature Branches

- `feature/login`
- `feature/search`
- `feature/payment`

### Bugfix Branch

- `bugfix/search-validation`

### Hotfix Branch

- `hotfix/payment-timeout`

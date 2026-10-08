# Two-Way Branching & Environment Workflow

This project follows a strict **Two-Way Branch Strategy** separating the **Testing Group** environment from the **Production** environment.

```
       [ Feature Work ]
              │
              ▼
    ┌───────────────────┐
    │  testing branch   │  ◄── Connected to Testing DB (isolated data)
    │  (Testing Group)  │      Run all tests, migrations & validations here
    └─────────┬─────────┘
              │ Verified & Tested
              ▼
    ┌───────────────────┐
    │ production branch │  ◄── Connected to Production DB (live data)
    │   (Live / Prod)   │      Never commit directly without testing first
    └───────────────────┘
```

---

## 1. Branch Roles

| Branch | Environment | Database | Purpose |
| :--- | :--- | :--- | :--- |
| **`testing`** | Testing Group (`APP_ENV=testing`) | `alabmovement_testing` | Development, integration testing, schema migrations preview, and QA validation. |
| **`production`** | Production (`APP_ENV=production`) | `alabmovement_production` | Live application for end users. Clean, audited, stable release code. |

---

## 2. Daily Workflow Guide

### Step 1: Work on the `testing` branch
Always check out the `testing` branch before making changes or testing new features:

```powershell
# Switch to the testing branch
git checkout testing

# Ensure you have the latest updates
git pull origin testing
```

### Step 2: Test against the testing database
Use `.env.testing` (or environment variables) to connect to your testing database instance:
- Run migrations against the testing database
- Verify your API endpoints, frontend, or backend logic
- Run automated unit or integration tests

```powershell
# Commit your tested changes to the testing branch
git add .
git commit -m "feat: implement new feature and verify on test DB"
git push origin testing
```

### Step 3: Promote tested changes to `production`
Once all tests pass on the testing branch and you are confident everything works:

```powershell
# Switch to production branch
git checkout production

# Pull latest production code
git pull origin production

# Merge verified changes from testing into production
git merge testing

# Push to the live production repository
git push origin production
```

### Step 4: Return to the `testing` branch
After completing the merge to production, switch back to `testing` for continued development:

```powershell
git checkout testing
```

---

## 3. Golden Rules

1. **Never commit untested code directly to `production`**.
2. **Never point the `testing` branch to the production database**.
3. **Database migrations must always be tested first on `testing`** before applying them to the live production database.

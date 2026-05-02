# Branch Protection Rules Configuration Guide

## Overview
This guide provides step-by-step instructions to set up branch protection rules for the SaaradhiGo-main repository's 5-level hierarchical branching strategy.

---

## 🔐 Branch Protection Rules Summary

| Branch | Rule Type | Approvals | Status Checks | Force Push | Dismissals |
|--------|-----------|-----------|---------------|------------|-----------|
| **main** | Strict | 2 Required | Required | ❌ No | Stale reviews dismissed |
| **release** | Strict | 1 Required | Required | ❌ No | Stale reviews dismissed |
| **staging** | Moderate | 1 Required | Required | ❌ No | Manual dismiss allowed |
| **testing** | Lenient | 0 | Required | ✅ Yes | Manual dismiss allowed |
| **develop** | Flexible | 0 | Optional | ✅ Yes | Manual dismiss allowed |

---

Once branch protection rules are set up, here's the flow:

```
1. Developer creates feature branch:
   git checkout -b feature/web-auth develop

2. Pushes changes and creates PR to develop
   → No approvals required (if configured)
   → Status checks run automatically

3. Merge to develop after checks pass

4. Once daily/weekly:
   PR: develop → testing (0 approvals, status checks)
   → QA team tests on testing branch

5. Once QA approves:
   PR: testing → staging (1 approval, all checks)
   → Pre-prod environment testing

6. Once staging verified:
   PR: staging → release (1 approval, all checks)
   → Release candidate ready

7. Final approval:
   PR: release → main (2 approvals, all checks, signed commits)
   → PRODUCTION DEPLOYMENT 🚀
```

---

## 📝 GitHub Actions CI/CD Status Checks

Add these status checks to your branch protection rules once configured:

- `build/web` - Web app build
- `test/web` - Web app tests
- `build/android` - Android build
- `test/android` - Android tests
- `build/ios` - iOS build
- `test/ios` - iOS tests
- `code-quality` - Linting & code coverage
- `security-scan` - Dependency security checks

---

For questions or issues, refer to GitHub's official documentation or contact your DevOps team.

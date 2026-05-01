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

## 🛠️ Step-by-Step Setup Instructions

### **STEP 1: Access Branch Protection Settings**

1. Navigate to your repository: `https://github.com/SaaradhiGo/SaaradhiGo-main`
2. Click **Settings** (gear icon) in the top right
3. In the left sidebar, click **Branches** (under "Code and automation" section)
4. You'll see "Branch protection rules" section
5. Click **Add rule** to create a new rule

---

## 📋 Branch Protection Rule Configurations

### **LEVEL 5: main (Production) - MOST STRICT** 🔒

**Branch name pattern:** `main`

**Settings to Enable:**

✅ **Require a pull request before merging**
   - Required approvals: **2**
   - Dismiss stale pull request approvals: ✅ **YES**
   - Require review from Code Owners: ✅ **YES**
   - Require approval of most recent reviewable push: ✅ **YES**

✅ **Require status checks to pass before merging**
   - Require branches to be up to date: ✅ **YES**
   - Status checks: (Add your CI/CD workflows)

✅ **Additional Protections**
   - Require conversation resolution: ✅ **YES**
   - Require signed commits: ✅ **YES** (Recommended)
   - Require linear history: ✅ **YES**
   - Allow force pushes: ❌ **NO**
   - Allow deletions: ❌ **NO**
   - Do not allow bypassing: ✅ **YES** (Applies to admins too)

---

### **LEVEL 4: release (Release Candidate) - STRICT** 🚀

**Branch name pattern:** `release`

**Settings to Enable:**

✅ **Require a pull request before merging**
   - Required approvals: **1**
   - Dismiss stale pull request approvals: ✅ **YES**
   - Require review from Code Owners: ✅ **YES**
   - Require approval of most recent reviewable push: ✅ **YES**

✅ **Require status checks to pass before merging**
   - Require branches to be up to date: ✅ **YES**
   - Status checks: (Add your CI/CD workflows)

✅ **Additional Protections**
   - Require conversation resolution: ✅ **YES**
   - Require signed commits: ⚠️ **Optional**
   - Require linear history: ✅ **YES**
   - Allow force pushes: ❌ **NO**
   - Allow deletions: ❌ **NO**
   - Do not allow bypassing: ✅ **YES**

---

### **LEVEL 3: staging (Pre-Production) - MODERATE** 📋

**Branch name pattern:** `staging`

**Settings to Enable:**

✅ **Require a pull request before merging**
   - Required approvals: **1**
   - Dismiss stale pull request approvals: ✅ **YES**
   - Require review from Code Owners: ⚠️ **Optional**

✅ **Require status checks to pass before merging**
   - Require branches to be up to date: ✅ **YES**
   - Status checks: (Add your CI/CD workflows)

✅ **Additional Protections**
   - Require conversation resolution: ⚠️ **Optional**
   - Require linear history: ⚠️ **Optional**
   - Allow force pushes: ❌ **NO**
   - Allow deletions: ❌ **NO**

---

### **LEVEL 2: testing (QA & Integration) - LENIENT** 🧪

**Branch name pattern:** `testing`

**Settings to Enable:**

✅ **Require a pull request before merging**
   - Required approvals: **0**
   - Dismiss stale pull request approvals: ✅ **YES**

✅ **Require status checks to pass before merging**
   - Require branches to be up to date: ✅ **YES**
   - Status checks: (Add your CI/CD workflows)

⚠️ **Additional Protections**
   - Allow force pushes: ✅ **YES** (For QA debugging)
   - Allow deletions: ⚠️ **Optional**

---

### **LEVEL 1: develop (Development) - FLEXIBLE** 🔄

**Branch name pattern:** `develop`

**Settings to Enable:**

✅ **Require status checks to pass before merging** (Optional)
   - Status checks: (Add your CI/CD workflows - non-blocking)

⚠️ **Flexible Protections**
   - Require a pull request: ⚠️ **Optional** (Team decision)
   - Allow force pushes: ✅ **YES** (For development flexibility)
   - Allow deletions: ✅ **YES**

---

## 🔄 Workflow Integration Example

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

## ✅ Verification Checklist

After setting up all rules:

- [ ] All 5 branches have protection rules
- [ ] main: 2 approvals, no force push, signed commits required
- [ ] release: 1 approval, no force push, linear history
- [ ] staging: 1 approval, status checks required
- [ ] testing: Status checks only, force push allowed for QA
- [ ] develop: Minimal restrictions, development-friendly

---

## 🔗 References

- [Managing a branch protection rule](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule)
- [About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)

---

## 📞 Support

For questions or issues, refer to GitHub's official documentation or contact your DevOps team.

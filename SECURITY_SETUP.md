# Repository Security Configuration Guide

This guide will help you complete the security setup to ensure **only you can approve and merge changes** to your repository.

## ✅ What's Already Done

- ✓ Comprehensive `.gitignore` - Blocks all user documents and personal data
- ✓ `SECURITY.md` - Complete data protection policy
- ✓ `CODEOWNERS` - Requires your approval on all changes
- ✓ `README.md` - Complete documentation

## 🔧 What You Need to Configure (GitHub Web UI Only)

These settings can only be configured through GitHub's web interface. Follow these steps:

---

## Step 1: Enable Branch Protection on `main`

1. Go to your repository: https://github.com/carlymariec/document_processing_pipeline
2. Click **Settings** (top right)
3. In the left sidebar, click **Branches**
4. Click **Add rule**
5. Fill out the form:

### Branch protection rule settings:

**Basic:**
- Branch name pattern: `main`

**Require a pull request before merging:**
- ✅ Require a pull request before merging (CHECKED)
- ✅ Require approvals (CHECKED)
  - Number of required reviews: `1`
- ✅ Require review from Code Owners (CHECKED)
- ✅ Require approval of the most recent reviewable push (CHECKED)

**Require status checks to pass before merging:**
- ✅ Require branches to be up to date before merging (CHECKED)

**Restrict who can push to matching branches:**
- ✅ Include administrators (CHECKED)
- ✅ Restrict who can push to matching branches (CHECKED)
- Select: **Only allow specified administrators to push**

6. Click **Create** button

### Result: ✅ Direct pushes to main are BLOCKED. All changes require PR + your approval.

---

## Step 2: Disable Forking (Prevents Unauthorized Copies)

1. Go to **Settings** → **General**
2. Scroll to **Danger Zone** section
3. Find "Forking"
4. Click **Disable forking**
5. Confirm the action

### Result: ✅ No one can fork your repo without your permission.

---

## Step 3: Enable Secret Scanning (Detects Leaked Credentials)

1. Go to **Settings** → **Code security and analysis**
2. Under "Secret scanning":
   - ✅ Enable "Secret scanning" (CHECKED)
   - ✅ Enable "Push protection" if available (CHECKED)
3. Under "Dependabot":
   - ✅ Enable "Dependabot alerts" (CHECKED)

### Result: ✅ Automatic detection of leaked API keys or credentials.

---

## Step 4: Configure Pull Request Settings

1. Go to **Settings** → **General**
2. Scroll to "Pull requests"
3. Configure:
   - ☐ Uncheck "Allow auto-merge"
   - Select default merge strategy: **Squash and merge** or **Rebase and merge**
   - ✅ Check "Automatically delete head branches"

### Result: ✅ No automatic merges; you maintain full control.

---

## Step 5: Require Commit Signatures (Optional but Recommended)

1. Go to **Settings** → **Branches**
2. Edit the `main` branch rule
3. Check: ✅ "Require signed commits"

### Result: ✅ All commits must be signed with GPG key (provides authenticity proof).

---

## Step 6: Configure Additional Security

### Repository Visibility:
1. Go to **Settings** → **General**
2. Visibility: Keep as **Public** (code visible, data protected by `.gitignore`)
3. Template repository: ☐ Unchecked

### Issue & Wiki Permissions:
1. Go to **Settings** → **General**
2. Configure:
   - ✅ Issues: Enabled (allows bug reports)
   - ✓ Wiki: Enabled (for documentation)
   - ☐ Discussions: Disabled (to reduce spam)

---

## 📋 Verification Checklist

After completing the above steps, verify these settings are in place:

### Main Branch Protection
- [ ] Branch protection rule exists for `main`
- [ ] Requires pull request before merge
- [ ] Requires 1 approval
- [ ] Requires code owner review (@carlymariec)
- [ ] Requires up-to-date branches
- [ ] Administrators included in restrictions
- [ ] Direct pushes to main are BLOCKED

### Repository Access Control
- [ ] Forking is DISABLED
- [ ] Secret scanning is ENABLED
- [ ] Push protection is ENABLED (if available)
- [ ] Auto-merge is DISABLED
- [ ] Default merge strategy is set

### Data Protection
- [ ] `.gitignore` blocks all user documents ✓
- [ ] `SECURITY.md` explains data policies ✓
- [ ] `CODEOWNERS` requires your review ✓
- [ ] No private data in public repo ✓

---

## 🔐 Security Architecture After Setup

```
┌─────────────────────────────────────────────────────┐
│         PUBLIC REPOSITORY (carlymariec/...)          │
│                                                      │
│  Code + Documentation (Safe to Share)               │
│  - Jupyter Notebook                                  │
│  - README.md                                         │
│  - SECURITY.md                                       │
│  - .gitignore                                        │
│  - CODEOWNERS                                        │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│              BRANCH PROTECTION (main)                │
│                                                      │
│  ✅ All changes require:                            │
│     1. Pull Request (not direct commit)              │
│     2. Code Review                                   │
│     3. Your Approval (@carlymariec)                  │
│     4. Code Owner Sign-Off                           │
│     5. Up-to-date with latest code                   │
│                                                      │
│  ❌ Prevented:                                       │
│     - Direct commits to main                         │
│     - Unsigned commits                               │
│     - Unreviewed merges                              │
│     - Forks without permission                       │
│     - Repository credential exposure                 │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│         USER LOCAL ENVIRONMENTS (PRIVATE)            │
│                                                      │
│  Protected by .gitignore:                           │
│  - User Documents (*.pdf, *.tiff, *.jpg, etc)      │
│  - Processed Files (*_searchable.pdf)               │
│  - Metadata Logs (*_metadata.txt)                   │
│  - Credentials (API keys, auth tokens)              │
│  - Temporary Data (/uploads, /temp, etc)            │
│                                                      │
│  Never committed to GitHub ✓                        │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 Typical Workflow After Setup

### If Someone Wants to Contribute:

1. **They fork the repo** → ❌ BLOCKED (forking disabled)
2. **They create a branch** → Allowed
3. **They make changes** → Changes saved locally
4. **They create a PR** → Pull request opened
5. **You review the PR** → You must approve
6. **You merge to main** → Changes deployed

### Result: **Only you can approve all changes to main branch**

---

## 🆘 Troubleshooting

### "I can't push directly to main"
✅ **This is correct!** Branch protection is working.
- Solution: Create a branch, make changes, push branch, create PR, approve PR, merge.

### "Secret scanning blocked my push"
✅ **This is correct!** Credentials were detected.
- Solution: Remove the credentials, regenerate them, push again.

### "I need to make an emergency fix"
✅ **You can override** as admin:
1. Go to branch protection rule
2. Temporarily uncheck "Include administrators"
3. Make your emergency commit
4. Re-enable the rule

---

## 📞 Questions?

Refer to:
- GitHub Docs: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/configuring-code-owners
- Branch Protection: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches

---

**Setup Complete!** Your repository is now fully secured. 🎉

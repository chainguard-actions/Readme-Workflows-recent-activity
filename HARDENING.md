<!-- markdownlint-disable -->

# Hardening Report: Readme-Workflows--recent-activity/v2.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Readme-Workflows--recent-activity/v2.4.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references across workflow files use mutable tags or branch names instead of immutable 40-character SHA commit hashes, making the workflows vulnerable to supply-chain attacks if the referenced action is compromised or its tag is moved.

Failing references:
- codeql-analysis.yml: actions/checkout@v3, github/codeql-action/init@v2, github/codeql-action/autobuild@v2, github/codeql-action/analyze@v2
- install.yml: actions/checkout@v3, actions/setup-node@v3, EndBug/add-and-commit@v9
- pr_comment.yml: actions/checkout@v3, peaceiris/actions-label-commenter@v1.10.0
- run-build.yml: actions/checkout@v3, actions/setup-node@v3, EndBug/add-and-commit@v9
- test-workflow.yml: actions/checkout@v3, Readme-Workflows/recent-activity@main
- update-readme.yml: actions/Checkout@v3, Readme-Workflows/recent-activity@main, lowlighter/metrics@v3.24
- update_changelog.yml: actions/checkout@v3, Readme-Workflows/readme-replacer@v1.0.1
- update_wiki.yml: actions/checkout@v3, Andrew-Chen-Wang/github-wiki-action@v3

Locations:

- `.github/workflows/codeql-analysis.yml:37`
- `.github/workflows/codeql-analysis.yml:42`
- `.github/workflows/codeql-analysis.yml:51`
- `.github/workflows/codeql-analysis.yml:63`
- `.github/workflows/install.yml:10`
- `.github/workflows/install.yml:12`
- `.github/workflows/install.yml:17`
- `.github/workflows/pr_comment.yml:18`
- `.github/workflows/pr_comment.yml:21`
- `.github/workflows/run-build.yml:14`
- `.github/workflows/run-build.yml:16`
- `.github/workflows/run-build.yml:25`
- `.github/workflows/test-workflow.yml:15`
- `.github/workflows/test-workflow.yml:18`
- `.github/workflows/update-readme.yml:14`
- `.github/workflows/update-readme.yml:16`
- `.github/workflows/update-readme.yml:24`
- `.github/workflows/update_changelog.yml:9`
- `.github/workflows/update_changelog.yml:10`
- `.github/workflows/update_wiki.yml:13`
- `.github/workflows/update_wiki.yml:15`

### missing-permissions (severity: medium)

These workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, workflows run with the repository's default token permissions (which may be broad), violating the principle of least privilege.

Locations:

- `.github/workflows/install.yml:1`
- `.github/workflows/pr_comment.yml:1`
- `.github/workflows/run-build.yml:1`
- `.github/workflows/test-workflow.yml:1`
- `.github/workflows/update-readme.yml:1`
- `.github/workflows/update_changelog.yml:1`
- `.github/workflows/update_wiki.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned `uses:` references across 8 workflow files by pinning to full 40-character SHA hashes (with original tag preserved as comment). Added top-level `permissions:` blocks to 7 workflow files that were missing them: install.yml (contents: write for commit/push), pr_comment.yml (contents: read, issues: write, pull-requests: write), run-build.yml (contents: write for commit/push), test-workflow.yml (contents: write for README update), update-readme.yml (contents: write for README update), update_changelog.yml (contents: write for changelog update), update_wiki.yml (contents: write for wiki update). The codeql-analysis.yml already had job-level permissions so only action pins were needed there.


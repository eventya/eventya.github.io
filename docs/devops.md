# Continuous Integration

This documentation explains the workflow for creating releases in our project using GitHub Actions. Below is a step-by-step explanation of its functionality, including branch naming conventions, PR requirements, and the automated tasks performed by the workflow.

## Purpose

This workflow automates the process of:

* Merging PRs into the `release/` branches.
* Generating release notes from merged PRs.
* Incrementing the version number.
* Tagging the release with the new version.
* Creating a GitHub release for future logs and reports.

## Diagram

To visualize the release process, we have created a diagram that outlines branch naming conventions, PR requirements, and the automated tasks handled by the GitHub Actions workflow.

**Figure 1: CI Workflow Diagram**

![CI Workflow Diagram](/images/workflow_diagram.png)

## 1. Branches naming convention

The project follows a clear branch naming convention for organization and consistency:

* **Feature Branches (`feature/`)**: Used for new functionality (e.g., `feature/add-user-authentication`).
* **Fix Branches (`fix/`)**: Used for bug fixes (e.g., `fix/avatar-display-error`).
* **Support Branches (`support/`)**: Used for infrastructure/configuration updates (e.g., `support/update-database-url`).
* **Release Branches (`release/`)**: Combines multiple feature, fix, and support branches for testing and deployment (e.g., `release/feature_user_auth_and_bug_fix`).

---

## 2. Pull Request (PR) Requirements

To ensure code quality, every PR must meet the following requirements:

* **Non-Technical Descriptions**: Each PR must include a clear explanation of the changes. Example: "Adds support for sending notification emails from the CMS."
* **Automated Testing**: All PRs must pass tests (e.g., RSpec, Rubocop) before merging.

---

## 3. Release Pipeline

This section outlines the key automated tasks in the release process:

1. **Create a Release Branch**: Developers merge multiple feature, fix, and support branches into a `release/` branch.
2. **Merge into `test_master`**: This triggers the GitHub Actions workflow to perform the following steps:

    * **Generate Release Notes**: Extract PR titles and descriptions into a `release_notes.txt` file.
    * **Increment Version**: Update the version in `version.txt` (e.g., `4.0.0` → `4.0.1`).
    * **Create a Git Tag**: Tag the release version (e.g., `v4.0.1`).
    * **Publish a GitHub Release**: Attach release notes and mark the release as stable.

---

## 4. Key Takeaways

* **Streamlined Workflow**: A consistent process for testing, merging, and releasing changes.
* **Automation**: Saves time by automating tasks like release notes, versioning, and tagging.
* **Transparency**: Clear descriptions ensure releases are easy to understand for technical and non-technical stakeholders.

---

## 5. Workflow Script Overview

This section breaks down the key parts of the GitHub Actions script.

### 5.1. Checkout Code

The workflow starts by checking out the repository's code. This ensures all required files, including `version.txt`, are available.

### 5.2. Fetch Merged PRs

The script fetches all PRs that have been merged into the `release/` branch. It identifies PRs based on merge commit messages and retrieves:

* Title
* Description
* PR Number

**Code Example:**

```javascript
const prList = [];
const releaseBranch = 'test_master';

// Fetch all closed PRs for the branch
const prs = await github.rest.pulls.list({
  owner: context.repo.owner,
  repo: context.repo.repo,
  state: 'closed',
  base: releaseBranch
});

// Sort and retrieve the latest PR
const latestPr = prs.data.sort((a, b) => new Date(b.created_at) - new Date(a.created_at))[0];
```

### 5.3. Generate Release Notes

The release notes are written to a file (`release_notes.txt`) for later use.

**Example contents of `release_notes.txt`:**

```
**Feature: Update Notifications** - #123: Adds notification updates to CMS.
**Bug Fix: Undefined Avatar** - #124: Fixes a bug causing undefined avatars.
```

### 5.4. Increment Version

The workflow reads the current version from `version.txt` and increments the patch version (the last digit) by 1.

**Code Example:**

```bash
VERSION=$(cat version.txt)
IFS='.' read -r -a parts <<< "$VERSION"
parts[2]=$((parts[2] + 1)) # Increment patch version
NEW_VERSION="${parts[0]}.${parts[1]}.${parts[2]}"
echo "$NEW_VERSION" > version.txt
```

### 5.5. Commit the Updated Version

The new version is committed to the repository with a message like:

```
Increment version to 4.0.1
```

### 5.6. Create a Git Tag

A Git tag is created using the incremented version (e.g., `v4.0.1`). This tag is used for the GitHub release.

### 5.7. Create GitHub Release

A GitHub release is created with the following information:

* **Tag Name**: The incremented version (e.g., `v4.0.1`).
* **Release Name**: "Release v4.0.1".
* **Release Notes**: The content from `release_notes.txt`.

---

## Conclusion

The Create Release workflow is a powerful system for managing software releases. It seamlessly integrates branch management, pull request tracking, versioning, and GitHub releases. By adopting this workflow, development teams can achieve:

* **Efficiency**: Automates tasks like generating release notes, incrementing versions, and tagging.
* **Clarity**: Non-technical descriptions and detailed release notes improve transparency for stakeholders.
* **Consistency**: A structured approach ensures that every release follows the same process.
* **Traceability**: Links to PRs and descriptions provide full visibility into each release.

By following this process, development teams can focus on delivering high-quality features and fixes while maintaining a transparent and predictable release process.

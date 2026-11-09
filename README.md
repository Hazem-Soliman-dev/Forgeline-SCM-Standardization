# ForgeLine DevOps Metrics Dashboard — Contribution Guidelines

Welcome to the **DevOps Metrics Dashboard** project[cite: 1]. As ForgeLine continues to build DevOps tooling for enterprise customers, this internal project must maintain strict Software Configuration Management (SCM) standards, baseline engineering hygiene, and disciplined contribution workflows[cite: 1, 2].


---

## 1. SCM & Feature Branch Isolation Strategy

### Why This Matters
Direct pushes to `main` disrupt baseline metrics platforms, destabilize production deployments, and introduce untraceable code regressions[cite: 1, 2]. Standardizing branch isolation guarantees that `main` remains continuously stable and production-ready[cite: 2].

### Core Idea
All development work must occur on short-lived feature branches tied 1-to-1 with specific GitHub Issues[cite: 2]. Code changes move strictly from isolated local branches to `main` via peer-reviewed Pull Requests[cite: 2].

### Key Terms
* **Protected Trunk (`main`):** The central source of truth for the codebase; direct pushes are disabled[cite: 2].
* **Feature Branch Isolation:** Dedicated branch (`feature/issue-<id>-<slug>`) created from stable `main` to isolate non-baseline work[cite: 2].

### Steps / Application
1. Synchronize your local baseline before starting work[cite: 2]:
   ```bash
   git switch main
   git pull origin main

2. Create and switch to an isolated feature branch:
   ```bash
   git switch -c feature/issue-<id>-<short-description>
   ```



---

## 2. GitHub Issue Management Workflow

### Why This Matters

Unscoped development leads to scope creep, unverified changes, and untraceable modifications during codebase maintenance.

### Core Idea

Every single modification to the project must originate from an assigned, scoped GitHub Issue before any code is written.

### Key Terms

* **GitHub Issue:** The canonical unit of work tracking problem statements, acceptance criteria, labels, and assignees.


* **Issue Labels:** Categorical tags (`bug`, `enhancement`, `documentation`) used to track project priority and scope.



### Steps / Application

1. Create or claim an existing Issue on GitHub.


2. Ensure the Issue details the **Problem Statement**, **Acceptance Criteria**, and correct **Labels**.


3. Assign yourself to the Issue before opening a corresponding feature branch.



---

## 3. Pull Request (PR) Governance & Code Review

### Why This Matters

Automated checks catch syntax errors, but human peer reviews prevent architectural flaws, maintainability debt, and unintended configuration regressions.

### Core Idea

Pull Requests act as formal quality contracts between feature branches and `main`, requiring passing automated CI checks and peer sign-offs before merging.

### Key Terms

* **Closing Keyword (`Closes #<id>`):** Metadata tag in the PR description that automatically closes the linked Issue upon merge.


* **Mandatory Peer Review:** Required code approval from team members before merging into the main branch.



### Steps / Application

1. Perform local pre-submission checks (`git status`, `git diff --staged`, and linter runs).


2. Push your feature branch to the remote repository:


```bash
git push -u origin feature/issue-<id>-<short-description>

```


3. Open a Pull Request targeting `main`.


4. Include `Closes #<id>` in the PR body and obtain at least 1 approving peer review before merging.



---

## 4. Local Quality Control & Debugging Standards

### Why This Matters

Scattering `print()` or `console.log()` lines clutters execution logs, risks leaking internal state, and introduces unformatted noise into PR review cycles.

### Core Idea

Developers must enforce automated formatters, static linters, and interactive IDE debuggers prior to submitting code for review.

### Key Guidelines

* **Pre-Submission Linting:** Always run local linters (`npm run lint:check` or `flake8 .`) and ensure an Exit Code `0` before staging edits.
* **Interactive Debugging:** Do not commit temporary print statements. Set **Breakpoints** inside your IDE and inspect the **Call Stack** to diagnose defects.
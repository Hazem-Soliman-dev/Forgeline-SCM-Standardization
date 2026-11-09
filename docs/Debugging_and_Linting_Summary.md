# ForgeLine Engineering: Pre-Submission Hygiene, Debugging & Linting Summary
*Project: DevOps Metrics Dashboard | Authority: Mateo Rossi, Engineering Manager*

---

## 1. Pre-Submission Code Verification (Linters)

### Why This Matters
Pushing unformatted code, syntax errors, or unused imports to remote Pull Requests creates noise in code reviews, degrades baseline engineering hygiene, and causes unnecessary continuous integration (CI) pipeline failures. Catching these errors locally reduces the feedback loop from minutes to milliseconds.

### Core Idea
Static analysis tools (Linters) parse source code Abstract Syntax Trees (AST) *without executing the program logic*. They systematically verify formatting, catch syntax bugs, detect dead variables, and enforce PEP 8 and company layout standards prior to code submission.

### Key Terms
* **Static Analysis / Linter:** An automated tool (`flake8`, `ESLint`) that inspects source code for style violations and structural defects without runtime execution.
* **Format-on-Save:** IDE feature that automatically formats code files upon saving, ensuring consistent styling.
* **Code Smells & Diagnostic Codes:** Standardized identifiers (e.g., `F401` for unused imports, `F841` for unused local variables) emitted by static checkers.

### Application Steps
1. Configure your local IDE with **Format-on-Save** enabled.
2. Run local linter validation before staging any modified files:
   ```bash
   # For Python modules:
   flake8 .
   
   # For Node / JS modules:
   npm run lint:check

3. Ensure linter exits with Code 0 before staging edits with git add.

---

## 2. Local Diff Review Practices

### Why This Matters

Accidentally committing temporary debug files, private credentials, or leftover logs risks security leaks and codebase pollution.

### Core Idea

Developers must perform line-by-line inspection of modifications across working copy and staging area boundaries before committing.

### Key Terms

* **Unstaged Diffs (`git diff`):** Compares working copy changes against Staging Area.
* **Staged Diffs (`git diff --staged`):** Compares Staging Index against latest HEAD commit.

### Application Steps

1. Run `git status` to detect untracked files.
2. Run `git diff` to audit unstaged local edits.
3. Run `git diff --staged` as a final security and cleanliness gate before `git commit`.

---

## 3. Interactive Debugging & Breakpoints

### Why This Matters

Using `console.log()` or `print()` pollutes production logs, risks accidental secret leakage, and provides limited insight into execution context.

### Core Idea

Interactive debuggers pause execution dynamically, enabling real-time inspection of call stack state and memory variables.

### Key Terms

* **Breakpoint:** An intentional pausing location inserted into source code via an IDE or debugger command.
* **Interactive Debugger:** A tool enabling line-by-line execution stepping (Step Into, Step Over, Step Out).

### Application Steps

1. Remove all temporary `print()` / `console.log()` lines.
2. Set a Breakpoint in your IDE on the target line of code.
3. Launch execution in Debug Mode.
4. Utilize debugger controls:
* **Step Over (F10):** Execute next line in current scope.
* **Step Into (F11):** Step inside called function.
* **Step Out (Shift+F11):** Resume until current function returns.
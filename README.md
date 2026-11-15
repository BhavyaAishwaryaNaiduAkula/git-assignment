# University Assignment: Git/GitHub Workflow & Software Testing

**Author:** Bhavya Aishwarya Naidu Akula  
**Course:** Software Engineering & Quality Assurance  
**Repository:** [https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment](https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment)  
**Final Submission Report:** [Download Report PDF](./Git_and_Software_Testing_Assignment_Report.pdf)

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Question 1: Git & GitHub Workflow (10 Marks)](#question-1-git--github-workflow-10-marks)
   - [Step 1: Project Setup & Initialization](#step-1-project-setup--initialization)
   - [Step 2: Sequential Workflow (Commits, Branching & Merging)](#step-2-sequential-workflow-commits-branching--merging)
   - [Step 3: .gitignore Configuration & Verification](#step-3-gitignore-configuration--verification)
   - [Step 4: Safe Commit Undo Operation](#step-4-safe-commit-undo-operation)
   - [Step 5: GitHub Remote Integration & Push](#step-5-github-remote-integration--push)
   - [Step 6: Git Commands Reference](#step-6-git-commands-reference)
3. [Question 2: Professional Test Case Suite for Login System](#question-2-professional-test-case-suite-for-login-system)
   - [Functional Requirements](#functional-requirements)
   - [Test Case Execution Table](#test-case-execution-table)
   - [Requirements Traceability Matrix (RTM)](#requirements-traceability-matrix-rtm)
4. [Final Verification Checklist](#final-verification-checklist)

---

## Project Overview
This repository contains the complete practical coursework submission covering advanced Git version control workflows and rigorous software quality assurance testing design. All operations were executed on a Windows 11 host using PowerShell, Git 2.53, and GitHub.

---

## Question 1: Git & GitHub Workflow (10 Marks)

### Step 1: Project Setup & Initialization
- Created directory `GitAssignment`
- Created semantic HTML pages: `index.html` and `about.html`
- Initialized local repository: `git init -b main`
- Confirmed files were untracked via `git status`

### Step 2: Sequential Workflow (Commits, Branching & Merging)
1. **Initial commit:**
   ```bash
   git add index.html about.html
   git commit -m "Initial project setup"
   ```
2. **Modify index.html & commit:**
   ```bash
   git add index.html
   git commit -m "Updated index page"
   ```
3. **Branch creation & checkout:**
   ```bash
   git branch feature
   git checkout feature
   ```
4. **Modify about.html on feature branch & commit:**
   ```bash
   git add about.html
   git commit -m "Added feature updates"
   ```
5. **Checkout main & merge feature:**
   ```bash
   git checkout main
   git merge feature
   ```
6. **Commit history log:**
   ```bash
   git log --oneline --graph --all
   ```

### Step 3: .gitignore Configuration & Verification
- Created `.gitignore` with rules:
  ```gitignore
  *.log
  temp/
  ```
- Created test directory `temp/` and test file `sample.log`.
- Verified exclusion with `git status` and `git check-ignore -v sample.log temp/temp_data.tmp`.
- Committed `.gitignore`:
  ```bash
  git add .gitignore
  git commit -m "Add .gitignore to ignore log files and temp directory"
  ```

### Step 4: Safe Commit Undo Operation
- Committed documentation snapshot:
  ```bash
  git add README.md
  git commit -m "Add project README"
  ```
- Undid ONLY the last commit while keeping working directory files 100% safe:
  ```bash
  git reset --soft HEAD~1
  ```
- Verified that `README.md` remained fully intact on disk and staged in the index, then re-committed.

### Step 5: GitHub Remote Integration & Push
- Provisioned public GitHub repository: `https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment`
- Connected remote:
  ```bash
  git remote add origin https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment.git
  git push -u origin main
  git push origin feature
  ```

### Step 6: Git Commands Reference
- Created [`git_commands.txt`](./git_commands.txt) detailing all 28 Git commands with technical explanations.
- Committed and pushed to GitHub.

---

## Question 2: Professional Test Case Suite for Login System

### Functional Requirements
- **FR-01:** Username cannot be empty.
- **FR-02:** Password minimum length is 6.
- **FR-03:** Correct credentials allow login.
- **FR-04:** Invalid credentials show appropriate error.
- **FR-05:** After 3 consecutive failed attempts, the account becomes locked.

### Test Case Execution Table

| Test Case ID | Test Scenario | Input Data | Expected Output (Specific) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC_LOGIN_001** | **Valid login** | Username: `student@bits.ac.in`<br>Password: `SecurePass2026!` | Display: `"Login successful. Redirecting to user dashboard..."` | **PASS** |
| **TC_LOGIN_002** | **Invalid username** | Username: `unknown_user_99`<br>Password: `SecurePass2026!` | Display: `"Invalid credentials: Username does not exist in the system."` | **PASS** |
| **TC_LOGIN_003** | **Invalid password** | Username: `student@bits.ac.in`<br>Password: `WrongPassword99` | Display: `"Invalid credentials: Incorrect password. Attempt 1 of 3."` | **PASS** |
| **TC_LOGIN_004** | **Both incorrect** | Username: `fake_user_007`<br>Password: `InvalidP@ss9` | Display: `"Invalid credentials: Username or password does not match."` | **PASS** |
| **TC_LOGIN_005** | **Empty username** | Username: `""` *(blank)*<br>Password: `SecurePass2026!` | Display: `"Username cannot be empty."` | **PASS** |
| **TC_LOGIN_006** | **Empty password** | Username: `student@bits.ac.in`<br>Password: `""` *(blank)* | Display: `"Password cannot be empty."` | **PASS** |
| **TC_LOGIN_007** | **Both empty** | Username: `""` *(blank)*<br>Password: `""` *(blank)* | Display: `"Username cannot be empty. Password cannot be empty."` | **PASS** |
| **TC_LOGIN_008** | **Password < 6 chars** | Username: `student@bits.ac.in`<br>Password: `Ab1#z` *(5 chars)* | Display: `"Password must be at least 6 characters in length."` | **PASS** |
| **TC_LOGIN_009** | **Password exactly 6 chars** | Username: `student@bits.ac.in`<br>Password: `P@s6x!` *(6 chars)* | Display: `"Login successful. Redirecting to user dashboard..."` | **PASS** |
| **TC_LOGIN_010** | **Three failed attempts lock** | Attempt 1: `BadPass1`<br>Attempt 2: `BadPass2`<br>Attempt 3: `BadPass3` | Attempt 1: `"Invalid credentials. Attempt 1 of 3."`<br>Attempt 2: `"Invalid credentials. Attempt 2 of 3."`<br>Attempt 3: `"Account locked due to 3 consecutive failed login attempts. Please contact support or reset password."` | **PASS** |
| **TC_LOGIN_011** | **Locked account access** | Username: `student@bits.ac.in`<br>Password: `SecurePass2026!` *(Locked)* | Display: `"Your account is currently locked. Authentication disabled. Please contact the administrator."` | **PASS** |
| **TC_LOGIN_012** | **Counter reset on success** | Att 1: `WrongPass` *(Fail 1/3)*<br>Att 2: `SecurePass2026!` *(Valid)* | Display: `"Login successful. Redirecting to user dashboard..."` (Counter reset to 0) | **PASS** |

---

## Final Verification Checklist

| Item | Requirement | Verification Result |
| :---: | :--- | :--- |
| ✓ | `index.html` created | **Verified & Live** |
| ✓ | `about.html` created | **Verified & Live** |
| ✓ | Git initialized | **Verified & Live** (`main` branch) |
| ✓ | Multiple commits exist | **Verified & Live** (8 commits) |
| ✓ | `feature` branch exists | **Verified & Live** (pushed to GitHub) |
| ✓ | Merge completed | **Verified & Live** (Fast-forward) |
| ✓ | `.gitignore` works | **Verified & Live** (`*.log`, `temp/`) |
| ✓ | Undo operation demonstrated | **Verified & Live** (`git reset --soft HEAD~1`) |
| ✓ | `git_commands.txt` created | **Verified & Live** (All 28 commands documented) |
| ✓ | Repository pushed to GitHub | **Verified & Live** |
| ✓ | Public GitHub URL copied | [https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment](https://github.com/BhavyaAishwaryaNaiduAkula/git-assignment) |
| ✓ | Test case table completed | **Verified & Live** (12 cases covering all requirements) |
| ✓ | Final PDF generated | [Git_and_Software_Testing_Assignment_Report.pdf](./Git_and_Software_Testing_Assignment_Report.pdf) |

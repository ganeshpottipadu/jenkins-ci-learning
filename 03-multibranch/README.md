# 03 - Multibranch Pipeline

This section demonstrates how Jenkins Multibranch Pipeline automatically discovers Git branches and creates separate Pipeline jobs based on the `Jenkinsfile` present in each branch.

## Objective

Understand how Jenkins automatically discovers branches from a GitHub repository, identifies branches containing a `Jenkinsfile`, and creates an independent Pipeline for each qualifying branch.

## Jenkins Job

**Multibranch Pipeline Job:**

```text
CI-Multibranch-SpringBoot
```

**Repository:**

```text
jenkins-ci-learning
```

**SCM:**

```text
GitHub
```

**Authentication:**

```text
SSH
```

**Credential:**

```text
github-ssh
```

## Multibranch Configuration

### Branch Source

```text
git@github.com:ganeshpottipadu/jenkins-ci-learning.git
```

### Branch Discovery

```text
Discover branches
```

### Build Configuration

```text
Mode: by Jenkinsfile
Script Path: Jenkinsfile
```

Jenkins checks each discovered branch for a file named:

```text
Jenkinsfile
```

Only branches containing a valid Jenkinsfile are considered for Pipeline creation.

---

## Initial Branch Discovery

The first repository scan discovered the `main` branch.

Jenkins confirmed:

```text
Checking branch main
'Jenkinsfile' found
Met criteria for branch: main
```

Jenkins then created a branch-specific Pipeline:

```text
CI-Multibranch-SpringBoot/main
```

The Pipeline executed successfully and generated an Allure report.

---

## Feature Branch Scenario

To understand how Multibranch Pipeline works with feature development, the following feature branch was created:

```text
feature/jenkins-multibranch
```

The branch was pushed to GitHub using:

```bash
git push -u origin feature/jenkins-multibranch
```

### First Jenkins Scan

During the first scan, Jenkins discovered the feature branch but reported:

```text
Checking branch feature/jenkins-multibranch
'Jenkinsfile' not found
Does not meet criteria
```

The `main` branch was still detected successfully:

```text
Checking branch main
'Jenkinsfile' found
Met criteria
```

### Why?

The feature branch did not yet contain the latest `Jenkinsfile`.

This demonstrated an important Multibranch Pipeline concept:

> Jenkins creates a branch Pipeline only when the branch meets the configured criteria, such as containing the required Jenkinsfile.

---

## Updating the Feature Branch

The latest GitHub changes were first fetched:

```bash
git fetch origin
```

The latest `origin/main` branch was then merged into the feature branch:

```bash
git merge origin/main
```

This brought the latest `Jenkinsfile` into:

```text
feature/jenkins-multibranch
```

The updated feature branch was then pushed to GitHub:

```bash
git push
```

---

## Second Jenkins Scan

Jenkins was manually instructed to scan the repository again.

This time Jenkins detected both branches successfully:

```text
Checking branch feature/jenkins-multibranch
'Jenkinsfile' found
Met criteria

Checking branch main
'Jenkinsfile' found
Met criteria
```

The scan completed with:

```text
Processed 2 branches
Finished: SUCCESS
```

Jenkins automatically created a separate Pipeline for:

```text
CI-Multibranch-SpringBoot/feature/jenkins-multibranch
```

---

## Feature Branch Build

The feature branch Pipeline was automatically scheduled and executed successfully.

### Build Result

```text
Branch: feature/jenkins-multibranch
Build: #1
Status: SUCCESS
```

The build also generated:

```text
allure-report.zip
```

and the Allure report was successfully published in Jenkins.

---

## Multibranch CI Flow

```text
Developer
    |
    v
GitHub Repository
    |
    v
Multiple Git Branches
    |
    v
Jenkins Multibranch Pipeline
    |
    v
Branch Discovery
    |
    v
Check for Jenkinsfile
    |
    +----------------------+
    |                      |
    | Jenkinsfile found?   |
    |                      |
    +----------+-----------+
               |
              Yes
               |
               v
      Create Branch Pipeline
               |
               v
         Checkout Code
               |
               v
             Build
               |
               v
             Test
               |
               v
         Allure Report
               |
               v
            SUCCESS
```

---

## Branch Structure

The GitHub repository contains multiple branches:

```text
jenkins-ci-learning
|
+-- main
|   |
|   +-- Jenkinsfile
|
+-- feature/jenkins-multibranch
    |
    +-- Jenkinsfile
```

Jenkins creates separate branch-specific Pipeline jobs:

```text
CI-Multibranch-SpringBoot
|
+-- main
|   |
|   +-- Build #1
|
+-- feature/jenkins-multibranch
    |
    +-- Build #1
```

Each branch has its own:

* Pipeline execution
* Build history
* Console output
* Workspace
* Allure report
* Build artifacts

---

## Why Multibranch Pipeline?

Without Multibranch Pipeline, a team might need to manually create separate Jenkins jobs for different branches.

For example:

```text
Jenkins Jobs

project-main
project-develop
project-feature-login
project-feature-payment
project-bugfix
```

With Multibranch Pipeline, one Jenkins job can manage multiple branches:

```text
CI-Multibranch-SpringBoot
|
+-- main
+-- develop
+-- feature/login
+-- feature/payment
+-- bugfix
```

Jenkins discovers the branches automatically and uses the Jenkinsfile stored in each branch.

---

## Real-World Scenario

In a development team, developers commonly work on multiple Git branches such as:

```text
main
develop
feature/login
feature/payment
bugfix/api-error
```

Each branch can contain its own version of the application and its own Jenkinsfile.

When Jenkins scans the repository, it discovers the branches and checks whether a Jenkinsfile exists.

If the Jenkinsfile is present, Jenkins creates a Pipeline for that branch.

This allows developers to validate their changes independently before merging them into the main branch.

---

## Branch Demonstration

This section is maintained on the `feature/jenkins-multibranch` branch to demonstrate how Jenkins Multibranch Pipeline detects and builds changes independently for each Git branch.



## Change Detection Experiment

To verify that Jenkins Multibranch Pipeline detects changes independently for each branch, a documentation change was made directly to the `feature/jenkins-multibranch` branch in GitHub.

### Steps Performed

1. Updated `03-multibranch/README.md` in the `feature/jenkins-multibranch` branch.
2. Committed the change directly to GitHub.
3. Opened Jenkins → `CI-Multibranch-SpringBoot`.
4. Selected **Scan Multibranch Pipeline Now**.
5. Jenkins scanned both `main` and `feature/jenkins-multibranch`.

### Jenkins Scan Result

Jenkins detected a new commit on the feature branch:

```text
Changes detected: feature/jenkins-multibranch
Scheduled build for branch: feature/jenkins-multibranch
```

The `main` branch was not rebuilt because Jenkins reported:

```text
No changes detected: main
```

The feature branch automatically triggered a new build.

### Result

`feature/jenkins-multibranch` Build #2 completed successfully.

This demonstrated that Jenkins Multibranch Pipeline:

* Detects changes independently for each branch.
* Identifies the branch containing the new commit.
* Automatically schedules a build for the changed branch.
* Does not trigger an unnecessary build for unchanged branches.
* Uses the `Jenkinsfile` from the respective branch to execute the Pipeline.

### Real-World CI Flow

```text
Developer pushes change
        ↓
GitHub feature branch updated
        ↓
Jenkins scans repository
        ↓
New commit detected
        ↓
Changed branch identified
        ↓
Branch-specific Pipeline triggered
        ↓
Build + Test + Allure Report
        ↓
Build SUCCESS
```

### Key Learning

Multibranch Pipeline allows Jenkins to manage CI independently for multiple branches in the same GitHub repository. Each branch can have its own Pipeline execution and build history while using the `Jenkinsfile` stored in that branch.


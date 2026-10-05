# Python CI with Jenkins

This section demonstrates a hands-on Continuous Integration workflow using Jenkins, GitHub, and Python.

## Objective

Run a Python script through Jenkins after retrieving the source code from a GitHub repository.

## Jenkins Job

**Job Name:** `CI-Python-Learning`  
**Job Type:** Freestyle Project

## Workflow

```text
GitHub
   ↓
feature/python-ci
   ↓
Jenkins SCM Checkout
   ↓
Python Script
   ↓
Console Output
   ↓
Build SUCCESS


## Python Application

Python script:
python-jenkins.py: The script prints a simple message to demonstrate successful Python execution through Jenkins.

Jenkins Configuration
Source Code Management
- SCM: Git
- Repository: git@github.com:ganeshpottipadu/jenkins-ci-learning.git
- Credentials: github-ssh
- Branch: */feature/python-ci
Build Step
Jenkins executes the Python script from the Jenkins workspace using the configured Python executable.
"C:\Users\ganes\AppData\Local\Python\bin\python.exe" "%WORKSPACE%\04-python-ci\python-jenkins.py"

Validation
The Jenkins build successfully:
1. Checked out the feature/python-ci branch from GitHub.
2. Retrieved python-jenkins.py into the Jenkins workspace.
3. Executed the Python script.
4. Displayed the Python output in the Jenkins Console.
5. Completed with Finished: SUCCESS.


## Real-World Use
Python scripts can be integrated with Jenkins to automate tasks such as:
- Configuration validation
- Health checks
- Data processing
- API-based automation
- Operational checks
- Report generation


This exercise demonstrates how Jenkins can retrieve Python source code from GitHub and execute it as part of a CI workflow.








Learning Outcome
This exercise demonstrates how Jenkins can retrieve Python source code from GitHub and execute it as part of a CI workflow.

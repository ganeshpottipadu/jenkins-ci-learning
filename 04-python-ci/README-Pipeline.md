# Python CI Automation Using Jenkins Declarative Pipeline

## 1. Project Overview

This project demonstrates how to automate Python script execution using Jenkins Declarative Pipeline integrated with GitHub.

The objective is to implement Pipeline as Code, where the entire CI workflow is defined in a Jenkinsfile and maintained in a GitHub repository.

## 2. Technologies Used

- Jenkins
- Git and GitHub
- Python 3
- Groovy (Jenkins Pipeline DSL)
- Windows Batch Commands

## 3. Project Structure

```text
04-python-ci/
│
├── README.md
├── README-Pipeline.md
├── python-jenkins.py
└── Jenkinsfile
```

## 4. Jenkins Pipeline Configuration

**Jenkins Job Name:** `CI-Python-Pipeline`

**Job Type:** Pipeline

### Source Code Management Configuration

| Configuration | Value |
|---|---|
| Definition | Pipeline script from SCM |
| SCM | Git |
| Repository | GitHub SSH repository |
| Credentials | github-ssh |
| Branch | feature/python-ci |
| Script Path | 04-python-ci/Jenkinsfile |

Jenkins retrieves the Jenkinsfile directly from the configured GitHub branch.

## 5. Jenkinsfile Implementation

The Jenkinsfile defines the complete execution workflow.

```groovy
pipeline {
    agent any

    stages {
        stage('Run Python Script') {
            steps {
                bat '"C:\\Users\\ganes\\AppData\\Local\\Python\\bin\\python.exe" "%WORKSPACE%\\04-python-ci\\python-jenkins.py"'
            }
        }
    }
}
```

### Explanation

**1. pipeline**

Defines the Declarative Pipeline structure.

**2. agent any**

Allows Jenkins to execute the Pipeline on any available agent.

**3. stages**

Contains the stages of the CI workflow.

**4. stage('Run Python Script')**

Defines the stage responsible for executing the Python application.

**5. steps**

Contains the commands executed within the stage.

**6. bat**

Executes the Windows batch command to run the Python script.

## 6. Pipeline Execution Workflow

1. Jenkins starts the Pipeline job.
2. Jenkins connects to the GitHub repository using SSH credentials.
3. Jenkins checks out the `feature/python-ci` branch.
4. Jenkins reads the Jenkinsfile from `04-python-ci/Jenkinsfile`.
5. Jenkins executes the Python script.
6. Jenkins captures the console output.
7. Jenkins displays the final build status.

## 7. Build Validation

**Job Name:** `CI-Python-Pipeline`

**Build Result:** SUCCESS

Expected Console Output:

```text
Hello from Jenkins!
Welcome, Ganesh
Python CI execution successful!
Finished: SUCCESS
```

The successful execution confirms that Jenkins can retrieve the Pipeline definition from GitHub and execute the Python script.

## 8. Key Learning Outcomes

Through this implementation, I learned:

- How to create a Jenkins Declarative Pipeline.
- How to integrate Jenkins with GitHub using SSH credentials.
- How to configure Pipeline script from SCM.
- How to maintain Jenkins Pipeline definitions in GitHub.
- How to execute Python scripts through Jenkins.
- How Jenkins stages and steps work.
- How to monitor Pipeline execution through Console Output.
- The fundamentals of Pipeline as Code.

## 9. Conclusion

Successfully implemented Python CI automation using Jenkins Declarative Pipeline integrated with GitHub.

This implementation demonstrates how CI workflows can be defined as code, version-controlled, and executed through Jenkins.

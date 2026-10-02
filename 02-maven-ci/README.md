# 02 - Maven CI

This section demonstrates Continuous Integration using Jenkins,
GitHub, Maven, and a Spring Boot application.

## Objective

Retrieve a Spring Boot application from GitHub using Jenkins
and build the application using Maven.



## Jenkins CI Implementation

The existing Jenkins Freestyle job was configured to retrieve the
Spring Boot application from GitHub and execute its Maven build.

### Jenkins Job

`CI-Freestyle-Learning`

### Application

`02-maven-ci/jenkins-demo`

### Build Command

```cmd
cd 02-maven-ci\jenkins-demo
mvnw.cmd clean test



### CI Flow

```text
Developer
    |
    | Push Code
    v
GitHub Repository
    |
    | SSH
    v
Jenkins
    |
    | Git Checkout
    v
Workspace
    |
    | Navigate to Project
    v
Spring Boot Application
    |
    | mvnw.cmd clean test
    v
Maven
    |
    +--> Clean
    |
    +--> Compile
    |
    +--> Run Tests
    |
    v
Build Result
    |
    +--> SUCCESS
    |
    +--> FAILURE

```
### Real-World Scenario

In a real development environment, a developer pushes changes to the GitHub repository. Jenkins retrieves the latest source code and executes the Maven build.
If the application compiles successfully and all tests pass, Jenkins marks the build as SUCCESS. If compilation or testing fails, the build is marked as FAILURE, allowing the team to identify issues before the code moves further in the development process.






## Jenkins Pipeline CI

A Jenkins Pipeline was created to automate the Spring Boot Maven CI process using a declarative Jenkinsfile.

### Pipeline Stages

1. **Checkout** – Jenkins retrieves the source code from GitHub using SSH credentials.
2. **Build** – Maven cleans the previous build artifacts using `mvn clean`.
3. **Test** – Maven executes the JUnit tests using `mvn test`.
4. **Check Allure Results** – Jenkins verifies that Allure test-result files were generated under `target/allure-results`.
5. **Allure Report** – Jenkins generates and publishes the Allure HTML test report.

### Jenkins Tools

* JDK: 21
* Maven: 3.9.16
* Source Control: GitHub
* CI Tool: Jenkins
* Test Framework: JUnit 5
* Test Reporting: Allure

### CI Flow

GitHub → Jenkins Checkout → Maven Clean → Maven Test → Allure Results → Allure Report

### Result

The Pipeline completed successfully and generated the Allure report in Jenkins.

### Key Learning

The Jenkins Pipeline acts as the automation layer that connects source-code checkout, Maven build execution, automated testing, and Allure reporting into a single repeatable CI workflow.





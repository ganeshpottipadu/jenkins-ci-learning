# Jenkins CI Learning Project

This repository documents my hands-on learning and implementation of
Continuous Integration (CI) using Jenkins and GitHub.

## Objective

Build a real-world CI workflow where application source code is maintained
in GitHub and Jenkins automatically retrieves, builds, and validates the code.

## Technologies

- Jenkins
- GitHub

## Learning Path

1. Jenkins Freestyle Project
2. Maven-based CI with Spring Boot
3. Jenkins Pipeline
4. Python CI
5. Jenkins Multibranch Pipeline

## Approach

Each implementation is documented with:

- Real-world scenario
- CI workflow
- Jenkins configuration
- Source code
- Build results
- Problems and troubleshooting
- Key learnings


## Allure Test Reporting

Allure was integrated into the Jenkins Maven CI workflow to provide
a visual test report after the automated tests are executed.

### Allure Components

The project uses:

- Allure JUnit 5 adapter
- Jenkins Allure Report plugin
- Allure Commandline

### Maven Dependency

The `pom.xml` was configured with the Allure JUnit 5 dependency:

```xml
<dependency>
    <groupId>io.qameta.allure</groupId>
    <artifactId>allure-jupiter</artifactId>
    <scope>test</scope>
</dependency>



### Jenkins Configuration 

Jenkins was configured with the Allure Commandline installation.

The Jenkins Maven job publishes the Allure report after the Maven test execution.

Developer
    |
    | Push Code
    v
GitHub
    |
    | SSH
    v
Jenkins
    |
    | Git Checkout
    v
Spring Boot Application
    |
    | Maven
    v
mvn clean test
    |
    v
JUnit 5 Tests
    |
    v
Allure Test Results
    |
    v
Allure Commandline
    |
    v
Allure HTML Report
    |
    v
Jenkins Allure Report


Build Result

The Jenkins build completed successfully with:

Tests Run: 1
Failures: 0
Errors: 0
Skipped: 0
Build Status: SUCCESS

The Allure report was successfully generated and published in Jenkins.

Key Learning

Allure does not replace JUnit or Maven.

JUnit executes the tests, Maven manages the build and test lifecycle, and Allure converts the test results into a visual report that can be viewed from Jenkins.











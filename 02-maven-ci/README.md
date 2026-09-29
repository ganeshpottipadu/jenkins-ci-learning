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











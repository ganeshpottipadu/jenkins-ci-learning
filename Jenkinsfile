pipeline {
    agent any

    tools {
        jdk 'JDK-21'
        maven 'Maven-3.9.16'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-ssh',
                    url: 'git@github.com:ganeshpottipadu/jenkins-ci-learning.git'
            }
        }

        stage('Build') {
            steps {
                bat '''
                    cd 02-maven-ci\\jenkins-demo
                    mvn clean
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                    cd 02-maven-ci\\jenkins-demo
                    mvn test
                '''
            }
        }

        stage('Check Allure Results') {
            steps {
                bat '''
                    echo ================================
                    echo Checking Allure Results
                    echo ================================

                    dir 02-maven-ci\\jenkins-demo\\target\\allure-results
                '''
            }
        }

        stage('Allure Report') {
            steps {
                allure([
                    includeProperties: false,
                    jdk: '',
                    results: [
                        [
                            path: '02-maven-ci/jenkins-demo/target/allure-results'
                        ]
                    ]
                ])
            }
        }
    }
}

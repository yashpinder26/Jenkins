pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'yashpindersaini@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - This stage compiles and packages the application using a build automation tool.'
                echo 'For Java projects, Maven (mvn clean package) or Gradle can be used.'
                echo 'For JavaScript projects, npm (npm run build) or yarn (yarn build) can handle the build process.'
                echo 'For Python projects, setuptools or PyInstaller can package the application..'
            }
        }

        stage('Unit & Integration Tests') {
            steps {
                echo 'Stage 2: Unit & Integration Tests - This stage runs unit tests to verify functionality and integration tests to ensure different components work together.'
                echo 'For Java projects, tools like JUnit, TestNG, or Selenium can be used for testing.'
                echo 'For JavaScript projects, Jest, Mocha, or Cypress can run tests.'
                echo 'For Python projects, pytest or unittest can handle testing.'
            }
            post {
                always {
                    script {
                        echo 'Sending email notification for test stage completion...'
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - This stage analyzes the code quality to ensure it meets industry standards and best practices.'
                echo 'For Java projects, tools like SonarQube, Checkstyle, and PMD can be used.'
                echo 'For JavaScript projects, ESLint and Prettier can check code quality.'
                echo 'For Python projects, pylint, flake8, or Black are useful for linting and code analysis.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - This stage scans the code for potential security vulnerabilities and risks.'
                echo 'Tools like OWASP Dependency-Check, Snyk, or Aqua Security Trivy can be used for security scanning.'
            }
            post {
                always {
                    script {
                        echo 'Sending email notification for security scan completion...'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - This stage deploys the application to a staging environment for further testing.'
                echo 'Deployment can be done using Docker, Ansible, or Kubernetes, depending on the project setup.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - This stage runs additional tests in the staging environment to simulate real-world usage.'
                echo 'For API testing, Postman or Newman CLI can be used.'
                echo 'For UI tests, Cypress or Selenium WebDriver can run tests.'
                echo 'For performance and load testing, Apache JMeter is a useful tool.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - This stage deploys the final tested version of the application to the production environment.'
                echo 'Docker and Kubernetes can handle container-based deployment.'
                echo 'For cloud environments, AWS CodeDeploy, Google Cloud Deployment Manager, or Azure Pipelines can be used.'
            }
        }
    }

    post {
        always {
            script {
                def buildStatus = currentBuild.currentResult
                def buildUser = currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')[0]?.userId ?: 'GitHub User'

                emailext(
                    subject: "Pipeline ${buildStatus}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """
                        <p>This is a Jenkins pipeline status.</p>
                        <p>Project: ${env.JOB_NAME}</p>
                        <p>Build Number: ${env.BUILD_NUMBER}</p>
                        <p>Build Status: ${buildStatus}</p>
                        <p>Started by: ${buildUser}</p>
                        <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    """,
                    to: "${EMAIL_RECIPIENTS}",
                    from: 'yashpindersaini@gmail.com',
                    replyTo: 'yashpindersaini@gmail.com'
                )
            }
        }
        failure {
            echo 'Pipeline failed. Sending notification email...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

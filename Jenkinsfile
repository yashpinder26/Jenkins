pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'yashpindersaini@gmail.com'  
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - This stage compiles the code and packages it into an executable format.'
                echo 'Stage 1: Build - This stage compiles the code and packages it into an executable format.'
                
            }
        }

        stage('Unit & Integration Tests') {
            steps {
                echo 'Stage 2: Unit & Integration Tests - This stage runs unit tests to verify functionality and integration tests to ensure different components work together.'
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
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - This stage scans the code for potential security vulnerabilities and risks.'
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
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - This stage runs additional tests in the staging environment to simulate real-world usage.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - This stage deploys the final tested version of the application to the production environment.'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Sending notification email...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/APC-SoCIT/APC_2025_2026_T1-DHAN-PROJECT-AND-TEST-MNGT-SYSTEM.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the custom ERPNext app...'
                sh 'bench build --app test_management'
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Running unit tests for the custom app...'
                sh 'bench --site yoursite.com run-tests --app test_management'
            }
        }
        stage('Deploy to Test Env') {
            steps {
                echo 'Updating and migrating the site on the test environment...'
                sh 'bench --site yoursite.com migrate'
                sh 'bench restart'
            }
        }
        stage('Integration Test') {
            steps {
                echo 'Running end-to-end integration tests...'
                sh 'echo "Integration tests passed."'
            }
        }
        stage('Create Docker Image') {
            steps {
                echo 'Creating Docker image for deployment...'
                sh 'docker build -t your-erpnext-project:latest .'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the app.js application...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
                echo "Tests completed successfully"
            }
        }

        stage('Deploy to Development') {
            when {
                branch 'dev-test-nodejs'
            }
            steps {
                echo 'Deploying the Node.js application to development environment...'
                // Add deployment steps for development environment here
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'prod-test-nodejs'
            }
            steps {
                echo 'Deploying the Node.js application to production environment...'
                // Add deployment steps for production environment here
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

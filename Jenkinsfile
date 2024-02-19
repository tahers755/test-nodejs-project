
pipeline {
    agent any

    environment {
        EC2_HOST = 'your_ec2_instance_ip'
        EC2_USER = 'your_ssh_username'
        EC2_KEY = credentials('your_ssh_private_key_credential_id')
    }

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
                script {
                    // Copy your application files to the EC2 instance
                    sshagent(['EC2_KEY']) {
                        sh "scp -i ${EC2_KEY} -o StrictHostKeyChecking=no -r . ${EC2_USER}@${EC2_HOST}:/path/to/your/remote/directory"
                    }

                    // Connect to the EC2 instance and execute deployment commands
                    sshagent(['EC2_KEY']) {
                        sh "ssh -i ${EC2_KEY} -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} 'cd /path/to/your/remote/directory && your_deployment_command'"
                    }
                }
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

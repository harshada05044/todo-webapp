pipeline {
    agent any

    environment {
        // Set any environment variables you need
        DEPLOY_ENV = "production"
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Pull the latest code from GitHub
                git 'https://github.com/harshada05044/todo-webapp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Set up virtual environment for Python if you're using it
                    sh 'python -m venv venv'
                    sh 'source venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Build Application') {
            steps {
                // Run the build command (for Python, this can be a lint/test command or packaging command)
                echo 'Building the application...'
            }
        }

        stage('Deploy to Server') {
            steps {
                script {
                    // Deploy the app to the target environment (this could involve SSH, FTP, or a cloud service API)
                    echo 'Deploying application to server...'
                    // Example SSH deployment (make sure SSH credentials are configured in Jenkins)
                    sshagent(['your-ssh-key-credentials-id']) {
                        sh 'scp -r * username@server:/path/to/deploy/directory'
                    }
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                echo 'Post-deployment checks...'
                // Optional: Perform post-deployment tasks like running tests on the deployed application
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline succeeded!'
        }

        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}

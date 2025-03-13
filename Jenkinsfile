pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage("Git Clone") {
            steps {
                script {
                    // Clean the workspace to avoid conflicts
                    deleteDir()
                }
                // Clone the repo explicitly from the main branch
                git branch: 'main', url: 'https://github.com/harshada05044/todo-webapp.git'
            }
        }

        stage("Build") {
            steps {
                bat 'mvn clean install'
            }
        }

        stage("Deploy") {
            steps {
                bat '''
                copy C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\first_pipeline\\webapp\\target\\webapp.war C:\\apache-tomcat-9.0.102\\apache-tomcat-9.0.102\\webapps
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Build or deployment failed! Check logs for details.'
        }
    }
}




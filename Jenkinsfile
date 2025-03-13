pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    environment {
        GITHUB_CREDENTIALS = credentials('github-token') // Fetch GitHub credentials
    }

    stages {
        stage("Git Clone") {
            steps {
                script {
                    deleteDir() // Clean workspace before cloning
                }
                git branch: 'main',
                    credentialsId: 'github-token',  // Use stored credentials
                    url: 'https://github.com/harshada05044/todo-webapp.git'
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





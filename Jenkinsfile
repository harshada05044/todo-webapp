#!groovy

pipeline {
    agent any

    environment {
        AZURE_RESOURCE_GROUP = 'python-webapp-rg'
        WEBAPP_NAME = "python-webapp"
        PACKAGE_NAME = "python-app-package.zip"
    }

    stages {
        stage('Workspace Cleanup') {
            steps {
                cleanWs()
                echo 'Cleaning workspace...'
            }
        }

        stage('Checkout Git Branch') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github-token',  // Use the correct credentials ID from Jenkins
                    url: 'https://github.com/harshada05044/python-flask-webapp.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Package Application') {
            steps {
                script {
                    // Zip all contents inside the project directory, excluding the root folder itself
                    sh "zip -r ${PACKAGE_NAME} ./*"
                    sh "zipinfo ${PACKAGE_NAME}"  // Verify the zip file
                }
            }
        }

        stage('Login to Azure') {
            steps {
                script {
                    withCredentials([azureServicePrincipal('jenkins-pipeline-sp')]) {
                        sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                        sh 'az webapp deploy --resource-group ${AZURE_RESOURCE_GROUP} --name ${WEBAPP_NAME} --src-path "${WORKSPACE}/${PACKAGE_NAME}"'
                    }
                }
            }
        }
    }
}



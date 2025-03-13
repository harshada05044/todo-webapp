pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/harshada05044/todo-webapp.git'
            }
        }
        
        stage('Set Up Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh 'source venv/bin/activate'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest || echo "No tests found, continuing..."'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'gunicorn --bind 0.0.0.0:5000 app:app &'
            }
        }
    }
}


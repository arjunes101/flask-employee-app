pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                    .venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask Application') {
    steps {
        sh 'docker run -d --name flask-app --network cicd-net -p 5000:5000 flask-employee-app'
    }
}
    }

    post {
        success {
            echo 'Flask application started successfully!'
        }
        failure {
            echo 'Pipeline execution failed!'
        }
    }
}

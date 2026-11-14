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
        sh '''
            pkill -f "python.*app.py" || true
            nohup .venv/bin/python app.py > flask.log 2>&1 &
            sleep 2
            curl -f http://localhost:5000/
        '''
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

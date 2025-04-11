pipeline {
    agent { label 'docker-agent-python' }

    environment {
        VENV_DIR = 'myapp/venv'
    }

    stages {
        stage('Build') {
            steps {
                echo '🔧 Setting up Python environment...'
                sh '''
                    cd myapp
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                    cd myapp
                    . venv/bin/activate
                    python3 hello.py
                    python3 hello.py --name=Brad
                '''
            }
        }

        stage('Deliver') {
            steps {
                echo '📦 Delivering...'
                sh '''
                    echo "🚀 Delivery step executed"
                '''
            }
        }
    }
}

pipeline {
    agent { label 'docker-agent-python' }

    parameters {
        string(name: 'NAME', defaultValue: 'World', description: 'Tên sẽ được truyền vào file hello.py')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Có muốn chạy bước Test không?')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'production'], description: 'Chọn môi trường để deploy')
    }

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
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo '🧪 Running tests...'
                sh """
                    cd myapp
                    . venv/bin/activate
                    python3 hello.py
                    python3 hello.py --name=${params.NAME}
                """
            }
        }

        stage('Deliver') {
            steps {
                echo "📦 Delivering to ${params.ENVIRONMENT} environment..."
                sh '''
                    echo "🚀 Delivery step executed"
                '''
            }
        }
    }
}

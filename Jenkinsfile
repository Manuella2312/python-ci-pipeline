pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Manuella2312/python-ci-pipeline.git'
            }
        }

        stage('Detect Docker') {
            steps {
                script {
                    def dockerExists = sh(script: 'command -v docker || true', returnStatus: true) == 0
                    if (dockerExists) {
                        echo "✅ Docker détecté, utilisation du conteneur Python"
                        env.USE_DOCKER = "true"
                    } else {
                        echo "⚠️ Docker non trouvé, fallback sur Python local"
                        env.USE_DOCKER = "false"
                    }
                }
            }
        }

        stage('Setup') {
            steps {
                script {
                    if (env.USE_DOCKER == "true") {
                        sh 'docker run --rm -v $PWD:/app -w /app python:3.11 pip install -r requirements.txt'
                    } else {
                        sh 'python3 -m venv venv'
                        sh '. venv/bin/activate && pip install -r requirements.txt'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (env.USE_DOCKER == "true") {
                        sh 'docker run --rm -v $PWD:/app -w /app python:3.11 pytest tests/'
                    } else {
                        sh '. venv/bin/activate && pytest tests/'
                    }
                }
            }
        }
    }
}
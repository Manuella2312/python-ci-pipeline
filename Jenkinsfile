pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Manuella2312/python-ci-pipeline.git'
            }
        }
        stage('Setup') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh '. venv/bin/activate && pytest tests/'
            }
        }
    }
}
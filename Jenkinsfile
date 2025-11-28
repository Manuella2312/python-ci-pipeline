pipeline {
    agent {
        docker {
            image 'python:3.11'
            args '-u' // mode non-buffered utile pour logs
        }
    }

    stages {
        stage('Préparation') {
            steps {
                echo 'Démarrage du pipeline Python...'
                sh 'python --version'
                sh 'pip --version'
            }
        }
        stage('Installation des Dépendances') {
            steps {
                sh 'python -m venv venv'
                sh '. venv/bin/activate && pip install --upgrade pip'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Exécution des Tests') {
            steps {
                sh '. venv/bin/activate && python -m unittest -v'
            }
        }
        stage('Nettoyage') {
            steps {
                echo 'Pipeline Python Terminé avec Succès.'
            }
        }
    }
}

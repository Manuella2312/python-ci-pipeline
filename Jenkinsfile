stage("Install dependencies") {
    steps {
        sh '''
        docker run --rm \
           -v $(pwd):/app \
           -w /app \
           python:3.11 \
           pip install -r requirements.txt
        '''
    }
}

stage("Run tests") {
    steps {
        sh '''
        docker run --rm \
           -v $(pwd):/app \
           -w /app \
           python:3.11 \
           python test_app.py
        '''
    }
}

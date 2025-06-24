pipeline {
    agent { 
        node {
            label 'docker-agent-python'  // your existing node
        }
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                // Run inside python docker container
                sh '''
                    docker run --rm -v $PWD/myapp:/app -w /app python:3.11-slim bash -c "
                        python3 -m venv venv &&
                        . venv/bin/activate &&
                        pip install -r requirements.txt
                    "
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    docker run --rm -v $PWD/myapp:/app -w /app python:3.11-slim bash -c "
                        . venv/bin/activate &&
                        python hello.py &&
                        python hello.py --name=Brad
                    "
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                    echo "doing delivery stuff.."
                '''
            }
        }
    }
}

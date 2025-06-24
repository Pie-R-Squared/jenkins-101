pipeline {
    agent { 
        node {
            label 'docker-agent-python'
        }
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                    cd myapp
                    # Install virtualenv locally for current user
                    python3 -m pip install --user virtualenv
                    
                    # Add local bin to PATH for this shell session
                    export PATH=$HOME/.local/bin:$PATH
                    
                    # Create virtual environment using virtualenv (not system venv)
                    virtualenv venv
                    
                    # Activate and install requirements
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
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
                echo 'Deliver....'
                sh '''
                    echo "doing delivery stuff.."
                '''
            }
        }
    }
}

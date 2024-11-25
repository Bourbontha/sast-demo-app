pipeline {
    agent {
        docker {
            image 'python:3.12'
            args '-u root'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Bourbontha/sast-demo-app.git', branch: 'master'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh '''
                python -m venv venv
                source venv/bin/activate
                pip install bandit
                '''
            }
        }
        stage('SAST Analysis') {
            steps {
                sh '''
                source venv/bin/activate
                bandit -f xml -o bandit-output.xml -r . || true
                '''
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Bourbontha/sast-demo-app.git', branch: 'master'
            }
        }
        stage('Install Python3-venv') {
            steps {
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y python3-venv'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh '''
                python3 -m venv venv
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

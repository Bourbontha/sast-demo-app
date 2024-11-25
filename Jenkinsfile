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
        stage('Install Bandit') {
            steps {
                sh 'pip install bandit'
            }
        }
        stage('SAST Analysis') {
            steps {
                sh 'bandit -r . -f xml -o bandit-output.xml || true'
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}

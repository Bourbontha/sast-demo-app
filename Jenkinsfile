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
                sh 'bandit -r . -f html -o bandit-report.html || true'
            }
        }
        stage('Publish Report') {
            steps {
                publishHTML(target: [
                    reportName: 'Bandit Report',
                    reportDir: '.',
                    reportFiles: 'bandit-report.html',
                    alwaysLinkToLastBuild: true,
                    keepAll: true
                ])
            }
        }
    }
}

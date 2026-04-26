pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f devops-container || true
                docker run -d -p 8080:80 --name devops-container devops-app
                '''
            }
        }

    }
}

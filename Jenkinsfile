pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "bharathyyy/myapp:latest"
  }

  stages {

    stage('Clone') {
      steps {
        git 'https://github.com/yourusername/your-repo.git'
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
        }
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build -t $DOCKER_IMAGE .'
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push $DOCKER_IMAGE'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f k8s/'
      }
    }

  }
}

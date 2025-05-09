pipeline {
agent any

stages {
    stage('Build') {
        steps {
            echo '1. Docker build'
            sh 'docker build --no-cache -t escuela-musica -f  Dockerfile .'
        }
    }
    stage('Deploy') {
        steps {
            echo '2. Deploy step'
            sh 'docker run -p 8081:80 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name escuela-musica '
        }
    }
  }
}
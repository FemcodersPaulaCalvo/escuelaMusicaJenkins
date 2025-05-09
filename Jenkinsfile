pipeline {
agent any

stages {
    stage('Build') {
        steps {
            echo '1. Docker build'
            sh 'docker build -t escuela-musica .'
        }
    }
    stage('Deploy') {
        steps {
            echo '2. Deploy step'
            sh 'docker run -d -p 8080:80 escuela-musica'
        }
    }
  }
}
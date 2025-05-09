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
            sh 'docker run -u root -d -p 8080:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11'
        }
    }
  }
}
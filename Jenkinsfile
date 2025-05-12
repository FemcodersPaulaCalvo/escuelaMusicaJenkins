pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS_ID = 'jenkinsLabToken3'
        DOCKER_CREDENTIALS_ID = 'jenkins1'
        DOCKER_IMG = 'escuela-musica2'
        DOCKERHUB_REPO = 'pcalvo/escuela-musica2'
    }

    stages {
        stage('Checkout github') {
            steps {
                echo '1. Github'
                git branch: 'jenkins2', credentialsId: "${GITHUB_CREDENTIALS_ID}", url: 'https://github.com/FemcodersPaulaCalvo/escuelaMusicaJenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo '2. Docker build'
                sh 'docker build --no-cache -t ${DOCKER_IMG}:latest -f Dockerfile .'
            }
        }

        stage('Tag img') {
            steps {
                echo '3. Tag img step'
                script {
                    env.TAG = "${env.BUILD_NUMBER}"
                    sh "docker tag ${DOCKER_IMG}:latest ${DOCKERHUB_REPO}:${env.TAG}"
                }
            }
        }

        stage('Push a Dockerhub') {
            steps {
                echo '4. Push dockerhub'
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${DOCKERHUB_REPO}:${env.TAG}
                            docker push ${DOCKER_IMG}:latest
                        """
                    }
                }
            }
        }
    }
}

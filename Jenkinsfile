pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "dolendra/my-k8s-app:${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Dolendra/jenkinslab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
    }
}

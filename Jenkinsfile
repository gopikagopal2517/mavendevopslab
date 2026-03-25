pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'your_username'
        IMAGE_NAME = 'my-devops-app'
    }
    stages {
        stage('Build Image') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:${env.BUILD_ID} ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_hub_login', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:${env.BUILD_ID}"
                }
            }
        }
    }
}

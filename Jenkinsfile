pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'YOUR_DOCKER_USERNAME'
    }
    stages {
        stage('Checkout GITHUB') {
            steps {
                git 'https://github.com'
            }
        }
        stage('Create Docker image') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/gold-rate-app:latest ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "docker login -u ${USER} -p ${PASS}"
                    sh "docker push ${DOCKER_HUB_USER}/gold-rate-app:latest"
                }
            }
        }
        stage('Create Cluster in Kubernetes') {
            steps {
                sh "kubectl apply -f deployment.yaml"
            }
        }
        stage('Show Deployed Application') {
            steps {
                sh "kubectl get service gold-service"
            }
        }
    }
}

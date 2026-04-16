pipeline {
    agent any
    stages {
        stage('Checkout GITHUB') {
            steps {
                git branch: 'main', url: 'https://github.com/Lohith260506/LABFAT.git'
            }
        }
        stage('Create Docker image') {
            steps {
                sh 'docker build -t YOUR_DOCKER_ID/gold-rate-app:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dhub-creds', passwordVariable: 'Lohith@2606', usernameVariable: 'lohith.s2023@vitstudent.ac.in')]) {
                    sh 'docker login -u $lohith.s2023@vitstudent.ac.in -p $Lohith@2606'
                    sh 'docker push lohith2606/gold-rate-app:latest'
                }
            }
        }
        stage('Create Cluster in Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}

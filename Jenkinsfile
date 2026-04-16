
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
                bat 'docker build -t lohith2606/gold-rate-app:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // USER and PASS are local variable names that Jenkins will fill
                withCredentials([usernamePassword(credentialsId: 'dhub-creds', passwordVariable: 'Lohith@2606', usernameVariable: 'lohith2606')]) {
                    // Use % to access variables in Windows 'bat'
                    bat "docker login -u %lohith2606% -p %Lohith@2606%"
                    bat "docker push lohith2606/gold-rate-app:latest"
                }
            }
        }
        stage('Create Cluster in Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
            }
        }
    }
}

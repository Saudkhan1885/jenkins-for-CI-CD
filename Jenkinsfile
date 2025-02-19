pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Saudkhan1885/jenkins-for-CI-CD.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t python-app .'
            }
        }
        
        stage('Deploy to Kubernetes') {
            agent {
                docker {
                    image 'bitnami/kubectl:latest'
                    args '--privileged' // Necessary for some Kubernetes actions
                }
            }
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}


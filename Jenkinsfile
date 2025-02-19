pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Saudkhan1885/jenkins-for-CI-CD.git'
            }
        }
        stage('Install kubectl') {
            steps {
                script {
                    // Install kubectl if not already installed
                    sh """
                    if ! command -v kubectl &>/dev/null; then
                        echo "kubectl not found, installing..."
                        curl -LO https://dl.k8s.io/release/v1.24.3/bin/linux/amd64/kubectl
                        chmod +x ./kubectl
                        sudo mv ./kubectl /usr/local/bin/kubectl
                    fi
                    """
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t python-app .'
            }
        }
        stage('Deploy to Kubernetes') {
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


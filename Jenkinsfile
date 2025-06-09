pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('kubeconfig')  // Add this in Jenkins as secret file
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/HrishiDarade/jenkins-k8s-deployment'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
        stage('Verify App') {
            steps {
                sh 'kubectl get pods'
                sh 'curl -s localhost:30085'
            }
        }
    }
    post {
        failure {
            echo '❌ Deployment failed!'
        }
        success {
            echo '✅ Deployment successful!'
        }
    }
}

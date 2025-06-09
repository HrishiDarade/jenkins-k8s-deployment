pipeline {
    agent any
    environment {
        KUBECONFIG = '/var/jenkins_home/.kube/config'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/HrishiDarade/jenkins-k8s-deployment'
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
                sh 'curl -s localhost:30085 || echo "App not reachable"'
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

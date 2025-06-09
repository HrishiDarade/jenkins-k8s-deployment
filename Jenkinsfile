pipeline {
    agent any
    environment {
        KUBECONFIG_CREDENTIALS = credentials('k8s-secret-file')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: KUBECONFIG_CREDENTIALS]) {
                        sh 'kubectl apply -f deployment.yaml'
                        sh 'kubectl apply -f service.yaml'
                    }
                }
            }
        }
        stage('Test Deployment') {
            steps {
                script {
                    sh 'kubectl get pods'
                    sh 'kubectl get services'
                }
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}

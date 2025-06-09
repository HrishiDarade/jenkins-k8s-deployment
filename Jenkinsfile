pipeline {
    agent any
    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'k8s-secret-file', variable: 'KUBECONFIG')]) {
                    sh '''
                    # Use the kubeconfig file to apply manifests
                    kubectl apply -f deployment.yaml --kubeconfig=$KUBECONFIG
                    kubectl apply -f service.yaml --kubeconfig=$KUBECONFIG
                    '''
                }
            }
        }
        stage('Test Deployment') {
            steps {
                withCredentials([file(credentialsId: 'k8s-secret-file', variable: 'KUBECONFIG')]) {
                    sh '''
                    # Verify the deployment
                    kubectl get pods --kubeconfig=$KUBECONFIG
                    kubectl get services --kubeconfig=$KUBECONFIG
                    '''
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

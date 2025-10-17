pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Yomi-Olaniyan/labapp.git'
            }
        }

        stage('Debug Workspace') {
            steps {
                echo "Current working directory:"
                sh 'pwd'
                echo "Files in workspace:"
                sh 'ls -la'
            }
        }

        stage('Deploy Application') {
            steps {
                echo "Deploying pending-pod.yaml..."
                sh 'kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f pending-pod.yaml'
            }
        }

        stage('Deploy kube-state-metrics') {
            steps {
                echo "Deploying kube-state-metrics..."
                sh '''
                    cd kubernetes-YAMLfiles/kube_state_metrics/standard
                    kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f .
                '''
            }
        }

        stage('Deploy Prometheus') {
            steps {
                echo "Deploying Prometheus..."
                sh '''
                    cd kubernetes-YAMLfiles/kube_state_metrics
                    kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f prometheus.yaml
                '''
            }
        }
    }

    post {
        success {
            echo "Application and monitoring stack deployed successfully."
        }
    }
}

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

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying pending-pod.yaml using full path..."
                sh 'kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f pending-pod.yaml'
            }
        }
    }
}

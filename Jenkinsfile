pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Yomi-Olaniyan/labapp.git'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl --kubeconfig=/var/lib/jenkins/.kube/config apply -f pending-pod.yaml'
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Jenkins will fetch the repo
                checkout scm
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                  echo "Applying all manifests from repo..."
                  kubectl apply -f .
                '''
            }
        }

        stage('Verify Rollout') {
            steps {
                sh '''
                  echo "Checking rollout status..."
                  kubectl rollout status deployment/web
                  kubectl rollout status deployment/app1
                  kubectl rollout status deployment/app2
                '''
            }
        }
    }
}


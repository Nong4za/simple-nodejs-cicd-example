pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: my-builder
    image: node:20-alpine
    command:
    - cat
    tty: true
"""
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test Env') {
            steps {
                container('my-builder') {
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }

        stage('Install') {
            steps {
                container('my-builder') {
                    sh 'npm ci'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}

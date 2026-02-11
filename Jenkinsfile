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

    environment {
        NODE_ENV = "production"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Environment') {
            steps {
                container('my-builder') {
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                container('my-builder') {
                    sh 'npm ci'
                }
            }
        }

        stage('Deploy to Vercel') {
            steps {
                container('my-builder') {
                    withCredentials([
                        string(credentialsId: 'DevOps18-vercel-token', variable: 'VERCEL_TOKEN')
                    ]) {
                        sh '''
                        npm install -g vercel
                        vercel pull --yes --environment=production --token=$VERCEL_TOKEN
                        vercel deploy --prod --token=$VERCEL_TOKEN
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ CI/CD Pipeline completed successfully'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}

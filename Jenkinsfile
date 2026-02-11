pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('DevOps18-vercel-token')
        VERCEL_PROJECT_NAME = 'simple-nodejs-cicd-example'
    }

    tools {
        // แก้ตรงนี้ครับ! จาก 'nodejs' เป็น 'NodeJS' ตามที่ Error แนะนำ
        nodejs 'NodeJS' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Node & npm') {
            steps {
                sh '''
                    node --version
                    npm --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                sh '''
                    npx vercel deploy \
                        --prod \
                        --yes \
                        --name $VERCEL_PROJECT_NAME \
                        --token $VERCEL_TOKEN
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deploy to Vercel SUCCESS'
        }
        failure {
            echo '❌ Deploy FAILED'
        }
    }
}
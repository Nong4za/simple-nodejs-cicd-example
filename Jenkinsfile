pipeline {
  agent {
    kubernetes {
      yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: node
    image: node:20-alpine
    command:
    - cat
    tty: true
'''
    }
  }

  environment {
    VERCEL_TOKEN = credentials('DevOps18-vercel-token')
  }

  stages {

    stage('Check Node & NPM') {
      steps {
        container('node') {
          sh 'node --version'
          sh 'npm --version'
        }
      }
    }

    stage('Install Dependencies') {
      steps {
        container('node') {
          sh 'npm ci'
        }
      }
    }

    stage('Deploy to Vercel') {
      steps {
        container('node') {
          sh '''
            npx vercel deploy \
              --prod \
              --confirm \
              --token $VERCEL_TOKEN
          '''
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

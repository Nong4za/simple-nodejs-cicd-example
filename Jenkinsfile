pipeline {
  agent any

  tools {
    nodejs 'NodeJS'
  }

  environment {
    VERCEL_TOKEN = credentials('DevOps18-vercel-token')
  }

  stages {

    stage('Check Node & npm') {
      steps {
        sh 'node --version'
        sh 'npm --version'
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
            --token $VERCEL_TOKEN
        '''
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished'
    }
  }
}

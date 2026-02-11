pipeline {
  agent {
    docker {
      image 'node:20-alpine'
      args '-u root'
    }
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

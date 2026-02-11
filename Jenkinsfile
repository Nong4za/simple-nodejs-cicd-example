stage('Deploy to Vercel') {
    steps {
        container('my-builder') {
            withCredentials([
                string(credentialsId: 'vercel-token', variable: 'VERCEL_TOKEN')
            ]) {
                sh '''
                npm install -g vercel

                vercel pull \
                  --yes \
                  --environment=production \
                  --project=simple-nodejs-cicd \
                  --scope=your-vercel-username \
                  --token=$VERCEL_TOKEN

                vercel deploy \
                  --prod \
                  --project=DevOps18-simple-nodejs \
                  --scope=nong4za \
                  --token=$VERCEL_TOKEN
                '''
            }
        }
    }
}

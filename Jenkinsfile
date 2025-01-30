pipeline {
  agent {
    docker {
      image 'node:16-buster-slim'
      args '-p 3000:3000'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') { 
      steps {
        sh './jenkins/scripts/test.sh' 
      }
    }
    stage('Deploy 🚀') { 
      steps {
        sh '''
          npm run build
          npx serve -s build -l 3000 &
          sleep 5
          sudo rm -rf ./node_modules
          echo "http://103.175.217.164:3000"
        '''
        // sh './jenkins/scripts/deliver.sh' 
        // input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
        // sh './jenkins/scripts/kill.sh' 
      }
    }
  }
}
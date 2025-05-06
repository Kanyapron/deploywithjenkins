pipeline {
  agent {
    docker {
      image 'node:18-alpine'
      args '-u root:root' // สำคัญ ถ้า permission error
    }
  }

  environment {
    FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        dir('frontend') { // ✅ ปรับตามโครงสร้างโปรเจกต์ของคุณ
          sh 'npm install'
        }
      }
    }

    stage('Build React App') {
      steps {
        dir('frontend') {
          sh 'npm run build'
        }
      }
    }

    stage('Install Firebase Tools') {
      steps {
        sh 'npm install -g firebase-tools'
      }
    }

    stage('Deploy to Firebase') {
      steps {
        dir('frontend') {
          sh 'firebase deploy --token "$FIREBASE_TOKEN"'
        }
      }
    }
  }

  post {
    success {
      echo '✅ Deploy Complete!'
    }
    failure {
      echo '❌ Deploy Incomplete!'
    }
  }
}

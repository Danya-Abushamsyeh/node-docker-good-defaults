pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/Danya-Abushamsyeh/node-docker-good-defaults.git', branch: 'main', changelog: true, poll: true)
      }
    }

    stage('Build Docker Images') {
      steps {
        sh 'docker build -t danyaabushameh/danya_q2:$BUILD_ID .'
      }
    }

  }
}
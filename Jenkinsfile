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

    stage('Run & Test the Containers') {
      steps {
        sh 'docker-compose up -d'
        sh 'sleep 5'
        sh 'curl http://localhost:3000'
      }
    }

    stage('Upload to DockerHub') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: '1692000', usernameVariable: 'danyaabushameh')]) {
          sh "docker login -u ${danyaabushameh} "
          sh 'docker-compose push'
        }

      }
    }

  }
}
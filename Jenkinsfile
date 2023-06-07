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
        sh 'docker stop danya2 && docker rm danya2'
        sh "docker run --name danya2 -d -p 3000:80 danyaabushameh/danya_q2:$BUILD_ID"
        sh 'sleep 15'
        sh 'curl http://localhost:80'
      }
    }

    stage('Upload to DockerHub') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: '1692000', usernameVariable: 'danyaabushameh')]) {
          sh "docker login -u ${danyaabushameh} "
          sh 'docker push danyaabushameh/danya_q2:$BUILD_ID'
        }

      }
    }

  }
}
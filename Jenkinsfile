pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lidorg-dev/node-docker-good-defaults']])
            }
        }
        
        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }
        
        stage('Run & Test the Containers') {
            steps {
                sh 'docker-compose up -d'
                sh 'sleep 5' // Wait for the containers to start up
                sh 'curl http://localhost:3000' // Perform tests on the running containers
            }
        }
        
        stage('Upload to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: '1692000', usernameVariable: 'danyaabushameh')]) {
                    sh "docker login -u ${danyaabushameh} "
                    sh "docker-compose push"
                }
            }
        }
    }
}


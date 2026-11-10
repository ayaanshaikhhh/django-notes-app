@Library('Shared') _
pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage('Hello'){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                sh 'whoami'
                echo 'Source code checked out successfully.'
            }
        }

        stage('Build') {
           steps{
               script{
                   build("ayaannnn","notes-app-jen","1.0")
               }
           }
        }

        stage('Push to DockerHub') {
            steps {
                script{
                    dockerhub_push()
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
    }
}






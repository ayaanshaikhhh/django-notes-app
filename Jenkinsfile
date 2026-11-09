@Library('Shared') _

pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage('Code Clone') {
            steps {
                sh 'whoami'
                clone(
                    'https://github.com/ayaanshaikhhh/django-notes-app.git',
                    'main'
                )
            }
        }

        stage('Code Build') {
            steps {
                dockerbuild('notes-app', 'latest')
            }
        }

        stage('Push to DockerHub') {
            steps {
                dockerpush('dockerHubCreds', 'notes-app', 'latest')
            }
        }

        stage('Deploy') {
            steps {
                deploy()
            }
        }
    }
}

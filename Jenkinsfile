pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage('Code') {
            steps {
                sh 'whoami'
                echo 'Source code checked out successfully.'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t notes-app:1.0 .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'DockerHubCred',
                        usernameVariable: 'DOCKERHUB_USER',
                        passwordVariable: 'DOCKERHUB_PASS'
                    )
                ]) {
                    sh '''
                        set -e

                        echo "$DOCKERHUB_PASS" | docker login \
                            -u "$DOCKERHUB_USER" --password-stdin

                        docker tag notes-app:1.0 ayaannnn/notes-app-jen:1.0
                        docker push ayaannnn/notes-app-jen:1.0

                        docker logout
                    '''
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

pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-test')
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build - t andrewsrepo/nana-app:latest .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push andrewsrepo/nana-app:latest'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
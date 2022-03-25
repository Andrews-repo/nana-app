pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred')
    }

    tools {nodejs "node"}

    stages {
        stage('New Build') {
            steps {
                sh 'npm install mocha'
            }
        }

        stage('test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t andrewsrepo/nana-app:$BUILD_NUMBER .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push andrewsrepo/nana-app:$BUILD_NUMBER'
            }
        }
        stage('Cleanup') {
            steps {
                sh 'docker rmi andrewsrepo/nana-app:$BUILD_NUMBER'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
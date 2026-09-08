pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t jenkins-demo-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker images jenkins-demo-app'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop jenkins-demo-app || true
                    docker rm jenkins-demo-app || true

                    docker run -d \
                        --name jenkins-demo-app \
                        -p 8081:80 \
                        jenkins-demo-app
                '''
            }
        }
    }
}

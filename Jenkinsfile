pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MattWoz02/coursework2'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('dockerfile:latest')
                }
            }
        }

        stage('Test Docker Image') {
            steps {
                script {
                    sh 'docker run dockerfile:latest'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'mattwoz02') {
                        docker.image('dockerfile:latest').push()
                    }
                }
            }
        }
       
    }
}

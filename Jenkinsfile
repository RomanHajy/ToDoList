pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/RomanHajy/to-do-list-ci-cd'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('romanhajy/to-do-list')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    bat """
                    echo %PASSWORD% | docker login -u %USERNAME% --password-stdin
                    docker push %USERNAME%/to-do-list
                    """
                }
            }
        }
    }
}

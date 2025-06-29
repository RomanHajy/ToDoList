pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ramanhajy/ToDoList'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('ramanismael/to-do-list')
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
                    script {
                        sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                        sh 'docker push $USERNAME/to-do-list'
                    }
                }
            }
        }
    }
}

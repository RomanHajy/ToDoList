pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/RomanHajy/ToDoList'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('romanhajy/todolist')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                        sh "docker push $USERNAME/to-do-list"
                    }
                }
            }
        }
    }
}

pipeline {
    agent any

    environment {
        IMAGE_NAME = "romanhajy/to-do-list"
    }

    stages {
        stage('Manual Git Clone') {
            steps {
                sh '''
                    rm -rf to-do-list
                    git clone https://github.com/RomanHajy/ToDoList.git to-do-list
                    cd to-do-list
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    cd to-do-list
                    docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    sh '''
                        echo $PASSWORD | docker login -u $USERNAME --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }
}

pipeline {

    agent any

    environment {
        IMAGE_NAME = 'riya123/flask-devops'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/USERNAME/flask-devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {

                withCredentials([
                    usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                    )
                ]) {

                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin

                    docker push $IMAGE_NAME:$BUILD_NUMBER
                    '''
                }
            }
        }
    }
}
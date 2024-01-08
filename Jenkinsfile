pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Init') {
            steps {
                sh 'echo Init Step'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'            }
        }

        stage('Build backend') {

            steps {
                dir('backend') {
                    sh 'sudo docker build -t $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID .'
                    sh 'sudo docker push $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID'
                    sh 'sudo docker rmi $DOCKERHUB_CREDENTIALS_USR/backend:$BUILD_ID'
                }

            }
        }

        stage('Build admin') {
            
            steps {
                dir('admin') {
                    sh 'sudo docker build -t $DOCKERHUB_CREDENTIALS_USR/admin:$BUILD_ID .'
                    sh 'sudo docker push $DOCKERHUB_CREDENTIALS_USR/admin:$BUILD_ID'
                    sh 'sudo docker rmi $DOCKERHUB_CREDENTIALS_USR/admin:$BUILD_ID'
                }
            }
        }
        stage('Build frontend') {
            
            steps {
                dir('frontend') {
                    sh 'sudo docker build -t $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID .'
                    sh 'sudo docker push $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID'
                    sh 'sudo docker rmi $DOCKERHUB_CREDENTIALS_USR/frontend:$BUILD_ID'
                }
            }
        }

        stage('logout') {
            steps {
                sh 'sudo docker logout'
            }
        }
    }
}
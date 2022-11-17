pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('rvnjssss-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            //git 'https://github.com/ravdy/nodejs-demo.git'
              git credentialsId: 'github', url: 'https://github.com/midathanasiva/nodejs-demo'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t rvnjssss/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push rvnjssss/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}


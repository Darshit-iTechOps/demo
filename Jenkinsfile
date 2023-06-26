pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerpass')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/darshitbhuva99/demo.git'
            }
        }

        stage('Build docker image') {
            steps {
                bat 'docker build -t aqueido/nodeapp .'
            }
        }
        
       
        stage('push image') {
            steps {
                script{
                    withCredentials([string(credentialsId: 'dockerpass', variable: 'dockerpass')]) {
                        bat 'docker login -u aqueido -p %dockerpass%'

}
                    bat 'docker push aqueido/nodeapp'
                }
                
            }
        }
    }

    post {
        always {
            bat 'docker logout'
        }
    }
}

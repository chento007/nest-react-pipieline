pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }


    stages  {


        stage('Build Image Back end and backend') {
            steps {        
                sh 'docker build -t chentochea/api-image:v1 ./apps/api/'
                sh 'docker build -t chentochea/client-image:v1 ./apps/client/'
                sh 'docker images -a'
            }     
        }



        // push image to docker hub
        stage('Push image to Docker Hub'){
            steps {

                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    
                    sh 'docker login --username \$registery_username --password \$registery_password docker.io'
                    
                    sh 'docker push chentochea/api-image:v1'
                    sh 'docker push chentochea/client-image:v1'

                    sh 'docker rmi chentochea/api-image:v1'
                    sh 'docker rmi chentochea/client-image:v1'
                }
            }
        }



        // deploy
        stage('Deploy application'){
            steps {
                sh 'docker compose up -d --build'
            }
        }

        // post notification
    }
}
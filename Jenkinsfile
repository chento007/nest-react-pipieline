pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }

    stages  {

        stage('Build Image Back end and backend') {
            steps {        
                sh 'docker build -t chentobank/api-image:$(git rev-parse --short HEAD) ./apps/api/'
                sh 'docker build -t chentobank/client-image:$(git rev-parse --short HEAD) ./apps/api/'
            }     
        }



        // push image to docker hub
        stage("Push image to Docker Hub"){
            steps {

                withCredentials([usernamePassword(credentialsId: 'gitlap-token', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    
                    sh 'docker login --username $registery_username --password $registery_password'

                    sh 'docker push chentobank/api-image:$(git rev-parse --short HEAD)'
                    sh 'docker push chentobank/client-image:$(git rev-parse --short HEAD) '

                    sh 'docker rmi chentobank/api-image:$(git rev-parse --short HEAD)'
                    sh 'docker rmi chentobank/client-image:$(git rev-parse --short HEAD)'
                }
            }
        }



        // // deploy
        // stage("Deploy application"){
        //     steps {
        //         sh 'docker compose up -d --build'
        //     }
        // }

        // post notification
    }
}
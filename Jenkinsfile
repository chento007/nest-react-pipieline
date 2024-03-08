pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }

    environment {
        API_IMAGE = "chentobank/api-image:$(git  rev-parse --short HEAD)"
        CLIENT_IMAGE = "chentobank/client-image:$(git rev-parse --short HEAD)"
    }
    stages  {

        stage('Build Image Back end and backend') {
            steps {        
                sh 'docker build -t $API_IMAGE ./apps/api/'
                sh 'docker build -t $CLIENT_IMAGE ./apps/api/'
            }     
        }



        // push image to docker hub
        stage("Push image to Docker Hub"){
            steps {

                withCredentials([usernamePassword(credentialsId: 'gitlap-token', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    
                    sh 'echo $registery_username'
                    sh 'docker login --username $registery_username --password $registery_password'
                    
                    sh 'docker push $API_IMAGE'
                    sh 'docker push $CLIENT_IMAGE '

                    sh 'docker rmi $API_IMAGE'
                    sh 'docker rmi $CLIENT_IMAGE'
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
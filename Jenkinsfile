pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }

    environment {
        API_IMAGE = ""
        CLIENT_IMAGE = ""
    }
    stages  {

        stage('Preparation') {
            steps {
                script {
                    env.API_IMAGE = "chentochea/api-image:" + sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                    env.CLIENT_IMAGE = "chentochea/client-image:" + sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                }
            }
        }

        stage('Build Image Back end and backend') {
            steps {        
                echo "${env.API_IMAGE}"
                sh "docker build -t ${env.API_IMAGE} ./apps/api/"
                sh "docker build -t ${env.CLIENT_IMAGE} ./apps/client/"
                sh "docker images -a"
            }     
        }



        // push image to docker hub
        stage("Push image to Docker Hub"){
            steps {

                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    
                    sh "echo ${registery_username}"
                    sh "docker login --username chentochea --password ${registery_password} docker.io"
                    
                    sh "docker push ${env.API_IMAGE}"
                    sh "docker push ${env.CLIENT_IMAGE}"

                    sh "docker rmi ${env.API_IMAGE}"
                    sh "docker rmi ${env.CLIENT_IMAGE}"
                }
            }
        }



        // deploy
        stage("Deploy application"){
            steps {
                sh 'docker compose up -d --build'
            }
        }

        // post notification
    }
}
pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }

    stages {

        // build image
        stage('Build Image') {

            stage('Back-end') {
                steps {
                    sh 'docker build -t chentobank/api-image:$(git rev-parse --short HEAD) ./apps/api/'
                }
            }

            stage('Front-end') {
                steps {
                    sh 'docker build -t chentobank/client-image:$(git rev-parse --short HEAD) ./apps/api/'
                }
            }
        }

        // push image to docker hub
        step("Push image to Docker Hub"){
            steps {

                withCredentials([usernamePassword(credentialsId: 'gitlap-token', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    
                    sh 'docker login --username $registery_username --password $registery_password'

                    stage('Back-end') {
                        steps {
                            sh 'docker push chentobank/api-image:$(git rev-parse --short HEAD) '
                        }
                    }

                    stage('Front-end') {
                        steps {
                            sh 'docker push chentobank/client-image:$(git rev-parse --short HEAD) '
                        }
                    }

                    sh 'docker logout'
                }
            }
        }



        // deploy
        step("Deploy application"){
            steps {
                sh 'docker compose up -d --build'
            }
        }

        // post notification
    }
}
pipeline {
    agent any

    tools {
        nodejs 'node-16.18.1'
    }

    stages {


        stage('Build Image') {

            steps {
                withCredentials([usernamePassword(credentialsId: 'gitlap-token', passwordVariable: 'registery_password', usernameVariable: 'registery_username')]) {
                    echo '==============build version============='
                    sh 'echo $passwordVariable'
                    sh 'echo password $registery_username'
                }
            }
        }


        // build image

        // push image to docker hub

        // deploy

        // post notification
    }
}
pipeline {
    agent any
    tools {
        nodejs 'node'
    }
    stages {
        stage('build app') {
            steps {
               script {
                   echo "building the application..."
                   sh 'npm install'
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    sh 'docker build -t <Docker Hub Username>/<Image Name>:<Tag> .'
                }
            }
}
        stage('deploy to DockerHub') {
            steps {
                   echo 'deploying docker image to dockerhub'
                   sh 'docker login -u <Docker Hub Username> -p <Docker Hub Password>'
                   echo 'tag the image for dockerHub'
                   sh 'docker tag <Docker Hub Username>/<Image Name>:<Tag>'
                   sh 'docker push <Docker Hub Username>/<Image Name>:<Tag>'
                 }
            }
        }
        stage('deploy to k8s cluster') {
            steps {
                withAWS(credentials: '<awscred>', region: '<region>'){
                echo 'deployment into kubernetes cluster'
                sh 'kubectl apply -f react.yml'
            }
        }    
    }
}
}

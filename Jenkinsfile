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
                    sh 'docker build -t <collens4>/<reactapp>:<1> .'
                }
            }
}
        stage('deploy to DockerHub') {
            steps {
                   echo 'deploying docker image to dockerhub'
                   sh 'docker login -u <collens4> -p <understand1@>'
                   echo 'tag the image for dockerHub'
                   sh 'docker tag <collens4>/<reactapp>:<1>'
                   sh 'docker push <collens4>/<reactapp>:<1>'
                 }
            }
        }
        stage('deploy to k8s cluster') {
            steps {
                withAWS(credentials: '<awscred>', region: '<us-east-2>'){
                echo 'deployment into kubernetes cluster'
                sh 'kubectl apply -f react.yml'
            }
        }    
    }
}
}

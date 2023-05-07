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
                   sh 'npm install -g npm@9.5.1'
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    sh 'docker build -t wolburg-frontend .'
                }
            }
}
        stage('deploy to ECR') {
            steps {
                 withAWS(credentials: 'moladipoawscred', region: 'us-east-2'){
                   echo 'deploying docker image to aws ecr...'
                   sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 844268948863.dkr.ecr.us-east-2.amazonaws.com'
                   echo 'tag the image for ecr'
                   sh 'docker tag wolburg-frontend:latest 844268948863.dkr.ecr.us-east-2.amazonaws.com/wolburg-frontend:latest'
                   sh 'docker push 844268948863.dkr.ecr.us-east-2.amazonaws.com/wolburg-frontend:latest'
                 }
            }
        }
        stage('deploy to k8s cluster') {
            steps {
                withAWS(credentials: 'jideawscred', region: 'us-east-1'){
                echo 'deployment into kubernetes cluster'
                sh 'kubectl apply -f wolburgfront-app.yml'
            }
        }    
    }
}
}

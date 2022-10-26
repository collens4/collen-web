pipeline {
  agent any
  stages {
    stage('Checkout code') {
      steps {
        git(url: 'https://github.com/EBEN4REAL/docker-app', branch: 'master')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Frontend unit tests') {
          steps {
            sh 'npm i'
          }
        }

      }
    }

  }
  tools {
    nodejs 'NODEJS'
  }
}
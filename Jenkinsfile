pipeline {
    agent any

    environment {
       CI = true
   }

    stages {
        stage ("Code pull"){
            steps{
                checkout scm
                bat 'npm install'
                bat 'cd client && npm install'
            }
        }

        stage('Compile Smart Contracts') {
              steps {
                  bat 'truffle compile'
              }
          }

      stage('Test Contracts') {
            steps {
                  bat "truffle test"
                  bat "cd client && npm test --no-watch"
            }
            post {
                always {
                    // Archive unit tests for the future
                    junit allowEmptyResults: true, testResults: 'junit-custom.xml'
                    junit allowEmptyResults: true, testResults: 'client/junit.xml'
                }
            }
        }

    }
}

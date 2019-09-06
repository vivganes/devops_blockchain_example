pipeline {
    agent any

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
                  bat "cd client && npm test"
            }
            post {
                always {
                    // Archive unit tests for the future
                    junit allowEmptyResults: true, testResults: 'junit-custom.xml'
                    junit allowEmptyResults: true, testResults: 'client/junit.xml'
                }
            }
        }

        stage('Deploy Smart Contracts') {
            steps {
                bat "truffle migrate"
            }
        }
    }
}

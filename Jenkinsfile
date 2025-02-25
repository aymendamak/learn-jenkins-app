pipeline {
    agent any

    environment {
        APP_ENV  = "DEV"
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reusenode true
                }
            }
            steps {
                sh '''
                    node --version
                    npm --version
                    npm build
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reusenode true
                }
            }
            steps {
                sh '''
                    npm test
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reusenode true
                }
            }
            steps {
                sh '''
                    npm install netlify --save-dev
                    npx netlify deploy --prod
                    echo "Deploying to netlify"
                '''
            }
        }
    }
}

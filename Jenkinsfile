pipeline {
    agent any

    stages {
        stage('build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    args '--user root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -lsa
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('test'){
            steps{
                sh 'npm test'
            }
        }
    }
}
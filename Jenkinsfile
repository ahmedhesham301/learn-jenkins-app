pipeline {
    agent any

    stages {
        stage('build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                chown -R 123:128 "/var/empty/.npm" 
                ls -lsa
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
    }
}
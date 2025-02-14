pipeline {
    agent any

    stages {
        // stage('build') {
        //     agent{
        //         docker{
        //             image 'node:18-alpine'
        //             args '--user root'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             ls -lsa
        //             node --version
        //             npm --version
        //             npm ci
        //             npm run build
        //             ls -la
        //         '''
        //     }
        // }
        stage('test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    args '--user root'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    test -f ./build/index.html
                    npm test
                '''
            }
        }
        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    serve -s build
                    npx playwright test
                    npm install -g serve
                '''
            }
        }
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
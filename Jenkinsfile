pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    rm -rf node_modules package-lock.json
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
             agent {
                 docker {
                    image 'node:18-alpine'
                    reuseNode true
                 }
             }
            steps {
                sh '''
                test -f build/index.html
                npm test
            '''
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}

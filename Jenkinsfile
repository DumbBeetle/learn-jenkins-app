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
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('test') {
                agent{
                    docker{
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                    steps {
                        sh '''
                            echo "Test Stage"
                            npm run test
                            test -f build/index.html
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

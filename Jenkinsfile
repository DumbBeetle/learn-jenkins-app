pipeline {
    agent any

    stages {
    /*
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
*/
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
        stage('E2E') {
                        agent{
                            docker{
                                image 'mcr.microsoft.com/playwright:v1.49.1-noble'
                                reuseNode true
                            }
                        }
                            steps {
                                sh '''
                                    npm install serve
                                    node_modules/.bin/serve -s build &
                                    sleep 10
                                    npx playwright test
                                '''

                            }
                }
    }
    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}

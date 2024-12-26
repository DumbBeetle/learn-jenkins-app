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
                        '''
                        sh 'if [ ! -e /build/index.html ]; then
                            exit 1
                            else
                                echo "file exist"
                            fi'
                    }
                }
    }
}

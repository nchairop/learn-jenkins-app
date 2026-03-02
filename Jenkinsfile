pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    rm -rf node_modules
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('test'){
            steps{
                sh '''
                if [ ! -f "build/output.txt" ]; then
                echo "ERROR: build/output.txt not found"
                exit 1
                fi
                '''
            }
        }
    }
}

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
          set -e

          echo "Node: $(node --version)"
          echo "NPM (before): $(npm --version)"

          # Pin npm to v9 (more stable than npm 10 in many CI envs)
          npm i -g npm@9
          echo "NPM (after): $(npm --version)"

          # Optional but helps reduce noise + flakiness
          npm config set fund false
          npm config set audit false

          rm -rf node_modules
          npm cache clean --force

          npm ci
          npm run build
        '''
      }
    }
  }
}
pipeline {
  agent {
    docker {
        image 'node:10-alpine'
        args '--name docker-node -p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
    }
}
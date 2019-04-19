pipeline {
  agent {
    label 'docker' 
  }
  stages {
    stage('Docker node test') {
      agent {
        docker {
          // Set both label and image
          label 'docker'
          image 'node:10-alpine'
          args '--name docker-node' // list any args
        }
      }
  }
}
      steps {
        // Steps run in node:7-alpine docker container on docker slave
        sh 'node --version'
      }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'    
            }
        }
    }
}
void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/aletheia-foundation/aletheia-app"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
    agent any
    tools { nodejs "node" }
    stages {
        stage('Build') {
            steps {
                echo 'build step'
                sh 'npm install'
            }
        }
        // stage('Test') {
        //     steps {
        //         echo 'test step'
        //         sh 'npm run test:ci'
        //         sh 'npm run test-truffle:ci'
        //     }
        // }
        stage('Generate app builds') {
            steps {
                echo 'Generate app builds step'
                sh 'npm run electron:linux'
                archiveArtifacts artifacts: 'app-builds/**', fingerprint: true
            }
        }
        stage('Deploy contracts') {
            steps {
                echo 'deploy contracts step'
            }
        }
    }
    post {
        success {
            setBuildStatus("Build complete", "SUCCESS");
        }
        failure {
            setBuildStatus("Build failed", "FAILURE");
        }
    }
}
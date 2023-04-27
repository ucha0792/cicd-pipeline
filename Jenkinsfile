pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        script {
          git credentialsId: 'github-id',
          url: 'https://github.com/ucha0792/cicd-pipeline',
          branch: "master",
          changelog: true,
          poll: true
        }

      }
    }

  }
  environment {
    registry = 'ucha0792/gitlab'
  }
}
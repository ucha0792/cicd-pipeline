pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        script {
          git credentialsId: 'github', url: 'https://github.com/ucha0792/cicd-pipeline'
        }

      }
    }

  }
  environment {
    cicd-pipeline = 'ucha0792/Jenkinsfile'
  }
}

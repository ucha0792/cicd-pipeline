pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        script {
          git credentialsId: 'github-id',
          url: 'https://github.com/ucha0792/cicd-pipeline',
          branch: 'main',
          changelog: true,
          poll: true
        }

      }
    }

    stage('Application Build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

  }
  environment {
    registry = 'ucha0792/gitlab'
  }
}
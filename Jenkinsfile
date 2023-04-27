pipeline {
  agent any
  tools {nodejs "nodejs"}
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
          sh 'nmp install'
      }
    }

    stage('Tests') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside {c ->
          sh 'test.sh'}
        }

      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Docker Image Push') {
      steps {
        script {
          docker.withRegistry('', 'dockerhub-id') {
            docker.image("${registry}:${env.BUILD_ID}").push('latest')
          }
        }

      }
    }

  }
  environment {
    registry = 'ucha0792/gitlab'
  }
}

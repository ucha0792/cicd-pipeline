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

    stage('aplication Build') {
      steps {
        sh 'chmod +x -R ./scripts/build.sh'
      }
    }

    stage('Tests') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside {c ->
          sh '/scripts/test.sh'}
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

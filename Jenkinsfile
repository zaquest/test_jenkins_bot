#!/usr/bin/env groovy

pipeline {
  agent any
  stages {
    stage('Deploy master') {
      when {
        branch 'master'
      }
      steps {
        sh 'echo master'
      }
    }

    stage('Deploy branch') {
      when {
        branch 'branch'
      }
      steps {
        sh 'echo branch && exit 1'
      }
    }
  }

  post {
    always {
      telegramSend(
        message: "${currentBuild.displayName} ${env.BRANCH_NAME} build was ${currentBuild.result}",
        chatId: -467484815
      )
    }
  }
}

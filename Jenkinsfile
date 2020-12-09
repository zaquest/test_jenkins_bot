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
        sh 'echo branch'
      }
    }
  }

  post {
    always {
      telegramSend(
        message: "${currentBuild.displayName} ${env.BRANCH_NAME} build was ${currentBuild.displayName}",
        chatId: -467484815
      )
    }
  }
}

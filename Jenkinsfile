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
      def changeLogSets = currentBuild.changeSets
      def changeLog = "";
      for (int i = 0; i < changeLogSets.size(); i++) {
          def entries = changeLogSets[i].items
          for (int j = 0; j < entries.length; j++) {
              def entry = entries[j]
              changeLog += "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
          }
      }
      telegramSend(
        message: "${env.BRANCH_NAME}: build ${currentBuild.displayName} status ${currentBuild.result}\n```${changeLog}```",
        chatId: -467484815
      )
    }
  }
}

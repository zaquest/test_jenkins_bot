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
        message: "${env.BRANCH_NAME}: build ${currentBuild.displayName} status ${currentBuild.result}\n```${getChangeLog()}```",
        chatId: -467484815
      )
    }
  }
}


@NonCPS
def getChangeLog() {
  def MAX_MSG_LEN = 100
  def changeLogSets = currentBuild.changeSets
  def changeLog = "";
  for (int i = 0; i < changeLogSets.size(); i++) {
      def entries = changeLogSets[i].items
      for (int j = 0; j < entries.length; j++) {
          def entry = entries[j]
          def truncated_msg = entry.msg.take(MAX_MSG_LEN)
          changeLog += "[${entry.commitId}] by ${entry.author}: ${truncated_msg}"
      }
  }
  if (!changeLog) {
    changeLog = "No changes"
  }
  return changeLog;
}

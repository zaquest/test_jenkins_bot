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
String getChangeLog() {
  def changeLogSets = currentBuild.changeSets
  def changeLog = [];
  for (int i = 0; i < changeLogSets.size(); i++) {
      def entries = changeLogSets[i].items
      for (int j = 0; j < entries.length; j++) {
          def entry = entries[j]
          def commitId = entry.getCommitId().take(6)
          changeLog << "* ${commitId} | ${truncate(entry.msg)} [${entry.author}]"
      }
  }
  if (!changeLog) {
    changeLog = 'No changes'
  }
  return changeLog.join('\n');
}

String truncate(String str) {
  def MAX_LEN = 10
  if (str.length() > MAX_LEN) {
    return str.take(MAX_LEN - 1) + '…'
  }
  return str
}

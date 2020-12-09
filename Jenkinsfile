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
}

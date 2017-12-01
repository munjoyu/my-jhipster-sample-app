pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo Build, updated little'
      }
    }
    stage('Backend') {
      parallel {
        stage('Unit') {
          steps {
            sh 'echo Backend'
          }
        }
        stage('Performance') {
          steps {
            sh 'echo Performance'
          }
        }
      }
    }
    stage('Frontend') {
      steps {
        sh 'echo Static Analysis'
      }
    }
    stage('Static Analysis') {
      steps {
        sh 'echo Static Analysis'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploy'
      }
    }
  }
}
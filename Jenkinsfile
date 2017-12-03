pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3-alpine'
          args '-v /root/.m2:/root/.m2'
        }
      }
      steps {
	sh 'mvn -B -DskipTests clean package'
	stash name: 'war', includes: 'target/**'
      }
    }

    stage('Backend') {
      agent {
        docker {
          image 'maven:3-alpine'
          args '-v /root/.m2:/root/.m2'
        }
      }

      steps {
        unstash 'war'
        sh 'mvn -B -DtestFailureIgnore test || exit 0'
        junit '**/surefire-reports/**/*.xml || exit 0'
        sh 'echo Static Analysis'
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
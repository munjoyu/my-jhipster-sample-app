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
        parallel(
          'Unit': {
            unstash 'war'
            sh 'mvn -B -DtestFailureIgnore test || exit 0'
            junit '**/surefire-reports/**/*.xml'
          },
          'Performance': {
            unstash 'war'
            sh 'echo ./mvnw -B gatling:execute'

          }
        )
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
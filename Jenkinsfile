pipeline {
  agent any
  stages {
    stage('build apps') {
      parallel {
        stage('app1') {
          steps {
            sh 'docker build -t app_1 app_1'
            sh 'docker run app_1'
          }
        }
        stage('app2') {
          steps {
            sh 'docker build -t app_2 app_2'
            sh 'docker run app_2'
          }
        }
      }
    }
    stage('test apps') {
      parallel {
        stage('app1') {
          steps {
            sh 'echo testing app 1'
          }
        }
        stage('app2') {
          steps {
            sh 'echo testing app 1'
          }
        }
      }
    }
    stage('deploy master') {
        when {
            expression { env.BRANCH_NAME.startsWith("master") }
        }
        steps {
            sh 'echo Deploying Master'
        }
    }
    stage('deploy release') {
        when {
            expression { env.BRANCH_NAME.startsWith("release") }
        }
        steps {
            sh 'echo Deploying Release'
        }
    }
    stage('deploy pull request') {
        when {
            expression { env.BRANCH_NAME.startsWith("PR") }
        }
        steps {
            sh 'echo Deploying Pull request'
        }
    }
    stage('set tag') {
      steps {
        script {
          sh 'git fetch --tags'
          sh 'git tag -l --contains HEAD > tags'
          env.TAG = readFile('tags')
        }
      }
    }
    stage('tag conditional step') {
      when {
        { environment name: 'TAG', value: 'do' }
      }
      steps {
          sh 'echo Do It!'
      }
    }
    stage('use credentials') {
      environment {
        SECRET_KEY = credentials('SECRET_KEY')
      }
      steps {
        sh 'echo $SECRET_KEY'
      }
    }
  }
}

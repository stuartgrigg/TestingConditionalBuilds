pipeline {
  agent any
  stages {
    stage('build and test apps') {
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
    stage('get branch') {
        steps {
            sh 'echo env.BRANCH_NAME'
        }
    }
    stage('deploy') {
        if (env.BRANCH_NAME.startsWITH("master")) {
            steps {
                sh 'echo Deploying Master'
            }
        }
        if (env.BRANCH_NAME.startsWITH("release")) {
            steps {
                sh 'echo Deploying Release'
            }
        }
        if (env.BRANCH_NAME.startsWITH("PR")) {
            steps {
                sh 'echo Deploying Pull Request'
            }
        }
    }
  }
}

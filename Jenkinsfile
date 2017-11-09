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
            sh 'echo $BRANCH_NAME'
            sh 'exit 2'
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
    stage('try stuff') {
        steps {
            sh './things.sh'
            script {
                print currentBuild.absoluteUrl
            }
            sh 'git fetch --tags'
            sh 'git tag -l --contains HEAD'
        }
    }
  }
}

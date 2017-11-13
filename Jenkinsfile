pipeline {
  agent any
  stages {
    stage('build and test apps') {
      steps {
        script {
          def arr = ['cup', 'mug']
          def artefacts = [:]
          def sha = sh(script:'git rev-parse HEAD', returnStdout: true).trim()
          for(i = 0; i < arr.size(); i += 1) {
              artefacts[arr[i]] = {
                node('k8s') {
                    sh "echo from k8s"
                }
              }
          }
          parallel artefacts
        }
      }
    }
  }
}

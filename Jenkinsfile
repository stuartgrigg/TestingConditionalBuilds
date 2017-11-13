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
                build job: 'Slave_Pipe', parameters: [string(name: 'commit', value: sha)], wait: true, propagate: true
              }
          }
          parallel artefacts
        }
      }
    }
  }
}

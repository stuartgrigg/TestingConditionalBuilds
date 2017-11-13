pipeline {
  agent any
  stages {
    stage('build and test apps') {
      steps {
        sh 'git rev-parse HEAD > sha_file'
        script {
          def arr = ['cup', 'mug']
          def artefacts = [:]
          def sha = readFile('sha_file').trim()
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

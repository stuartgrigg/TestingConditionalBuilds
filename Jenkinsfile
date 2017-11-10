pipeline {
  agent any
  stages {
    stage('build and test apps') {
      steps {
        script {
          def arr = ['cup', 'mug']
          def artefacts = [:]
          for(i = 0; i < arr.size(); i += 1) {
              artefacts["Test${i}"] = {
                build job: 'Slave_Pipe', parameters: [string(name: 'myVariable', value: 'there')], wait: true, propagate: true
              }
          }
          parallel artefacts
        }
      }
    }
  }
}

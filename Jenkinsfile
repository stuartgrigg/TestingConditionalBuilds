pipeline {
  agent any
  stages {
    stage('build and test apps') {
      build job: 'Slave_Pipe', parameters: [string(name: 'myVariable', value: 'there')], wait: false, propagate: true
      echo 'done'
    }
  }
}

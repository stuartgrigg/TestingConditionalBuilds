pipeline {
  agent any
  stages {
    stage('build and test apps') {
      steps {
        build job: 'Slave_Pipe', parameters: [string(name: 'myVariable', value: 'there')], wait: true, propagate: true
        echo 'done'
      }
    }
  }
}

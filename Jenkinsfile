pipeline {
  agent any
  stages {
    stage('build and test apps') {
      environment {
          GITHUB = credentials('060047e8-a5b1-4926-a9c8-29e19b8a0948')
      }
      steps {
        script {
          def arr = ['cup', 'mug']
          def artefacts = [:]
          def sha = sh(script:'git rev-parse HEAD', returnStdout: true).trim()
          for(i = 0; i < arr.size(); i += 1) {
              def artefact = arr[i]
              artefacts[arr[i]] = {
                node('k8s') {
                    sh "echo ${artefact}"
                    sh "echo ${sha}"
                    sh 'git clone https://${GITHUB_PSW}@github.com/stuartgrigg/TestingConditionalBuilds.git'
                    sh """
                      cd TestingConditionalBuilds
                      git reset --hard ${sha}
                      ls -l
                    """
                }
              }
          }
          parallel artefacts
        }
      }
    }
  }
}

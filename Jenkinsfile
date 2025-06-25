pipeline {
      agent any
 tools {
    nodejs 'NodeJS installations'
}

      stages {
          stage('setup') {
            steps {
                browserstack(credentialsId: 'c0a615d1-bcd6-4909-9043-fcca87fd1421') {
                    // add commands to run test
                    // Following are some of the example commands -----
                    sh 'npm install'
                    sh 'browserstack-node-sdk jest src/sample.test.js'
                }
            }
           
          }
        }
      }

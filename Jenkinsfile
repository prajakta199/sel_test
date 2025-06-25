pipeline {
  agent any
  tools {
    nodejs 'NodeJS 18' // or whatever you’ve configured in Jenkins (can skip if not using SDK CLI)
  }
  environment {
    BROWSERSTACK_CRED_ID = 'c0a615d1-bcd6-4909-9043-fcca87fd1421' // Your BrowserStack credential ID (plugin-specific)
  }
  stages {
    stage('Install BrowserStack SDK') {
      steps {
        sh 'npm install -g browserstack-sdk'
      }
    }

    stage('Run Selenium TestNG Tests on BrowserStack') {
      steps {
        withCredentials([
          [$class: 'BrowserStackCredentials', credentialsId: env.BROWSERSTACK_CRED_ID]
        ]) {
          // SDK picks up BROWSERSTACK_USERNAME and BROWSERSTACK_ACCESS_KEY automatically
          sh 'npx browserstack-sdk --sync'
        }
      }
    }
  }
}

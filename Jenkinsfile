pipeline {
  agent any
  environment {
    BS_CREDENTIAL_ID = 'c0a615d1-bcd6-4909-9043-fcca87fd1421' // Replace with your actual credential ID
  }
  stages {
    stage('Run on BrowserStack') {
      steps {
        script {
          withCredentials([
            usernamePassword(
              credentialsId: env.BS_CREDENTIAL_ID,
              usernameVariable: 'BROWSERSTACK_USERNAME',
              passwordVariable: 'BROWSERSTACK_ACCESS_KEY'
            )
          ]) {
            // ✅ Actual Maven command to trigger build
            sh 'mvn clean test -Dbrowserstack.username=$BROWSERSTACK_USERNAME -Dbrowserstack.accesskey=$BROWSERSTACK_ACCESS_KEY -DsuiteXmlFile=testng.xml'
          }
        }
      }
    }
  }
}

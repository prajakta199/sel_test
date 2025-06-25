pipeline {
    agent any

    environment {
        cred = 'c0a615d1-bcd6-4909-9043-fcca87fd1421'  // Set your credentials ID here
    }

    tools {
        maven 'Maven 3.8.6'
        jdk 'JDK 11'
    }

    stages {

        stage('Run Selenium TestNG Tests on BrowserStack') {
            steps {
                script {
                    browserstack(credentialsId: "${env.cred}") {
                        sh 'mvn clean test -Dsurefire.suiteXmlFiles=config/sample-test.testng.xml'
                    }
                }
            }
        }
    }
}

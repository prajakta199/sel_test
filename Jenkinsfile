pipeline {
    agent any

    tools {
        
        jdk 'JDK 11'
    }

    stages {

        stage('Run Selenium TestNG Tests on BrowserStack') {
            steps {
                script {
                    browserstack(credentialsId: "test_bstack") {
                        sh 'mvn clean test -Dsurefire.suiteXmlFiles=config/sample-test.testng.xml'
                    }
                }
            }
        }
    }
}

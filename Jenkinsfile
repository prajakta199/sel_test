pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'  // Make sure this matches your Jenkins Global Tool name
        jdk 'JDK 11'         // Ensure JDK 11 is installed and named correctly in Jenkins
    }

    stages {

        stage('Run Selenium TestNG Tests on BrowserStack') {
            steps {
                browserstack(credentialsId: 'c0a615d1-bcd6-4909-9043-fcca87fd1421') {
                    // Run Maven test with specific TestNG XML
                    sh 'mvn clean test -Dsurefire.suiteXmlFiles=sample-test.testng.xml'
                }
            }
        }

    }
}

pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'  // your Maven tool name
        jdk 'JDK 11'         // your JDK tool name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Selenium TestNG Tests on BrowserStack') {
            steps {
                browserstack(credentialsId: 'c0a615d1-bcd6-4909-9043-fcca87fd1421	') {
                    sh 'mvn clean test'
                }
            }
        }

        stage('Publish Reports') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}

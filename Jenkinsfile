pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'  // your configured Maven installation name
        jdk 'JDK 11'         // your configured JDK installation name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run BrowserStack Tests') {
            steps {
                // Pass your BrowserStack credential ID configured in Jenkins BrowserStack plugin UI
                browserstack(credentialId: 'bs-cred-id-from-jenkins-ui') {
                    sh 'mvn clean test'
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}

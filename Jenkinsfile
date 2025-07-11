

pipeline {
   agent any
 tools {
        maven 'Maven 3.8.6'
        jdk 'JDK 11'
    }

    stages {
        stage('Read Jenkinsfile') {
            when {
                expression {
                    return params.Refresh == true
                }
            }
            steps {
                echo "Jenkinsfile reloaded successfully and Exiting early"
            }
        }

        stage('Copy Archive JAR') {
            when {
                expression {
                    return params.Refresh == false
                }
            }
            steps {
                script {
                    step([$class: '',
                          projectName: '',
                          fingerprintArtifacts: true,
                          target: 'libs'
                    ])
                }
            }
        }

        stage('Execute Web Browsers') {
            when {
                expression {
                    return params.Refresh == false
                }
            }

            steps{
                script{
                    browserstack(credentialsId: "test_bstack"){
                        unzip zipFile: 'libs/archive-jar.zip', dir: 'libs'
                        sh 'mvn clean test -Dsurefire.suiteXmlFiles=config/sample-test.testng.xml'

                       
                     
                            }
                        }
                    }
                }
            }
        }
    

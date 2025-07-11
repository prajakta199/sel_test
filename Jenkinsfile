

pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
            dir 'jenkins'
        }
    }

    environment {

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
                        web.each{
                            if(it.value){
                                stage(it.key){
                                    def exebrowser="${it.key}"
                                    stage("Running ${GroupsToRun} TestGroups"){
                                        dir(env.WORKSPACE){
                                            catchError(buildResult:'FAILURE', stageResult:'FAILURE'){
                                                sh 'mvn clean test -Dsurefire.suiteXmlFiles=config/sample-test.testng.xml'

                                            }

                                            }
                                            sh ""
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}

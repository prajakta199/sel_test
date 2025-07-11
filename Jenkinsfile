

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
                    browserstack(credentialsId: "browserstack-api-creds"){
                        unzip zipFile: 'libs/archive-jar.zip', dir: 'libs'
                        web.each{
                            if(it.value){
                                stage(it.key){
                                    def exebrowser="${it.key}"
                                    stage("Running ${GroupsToRun} TestGroups"){
                                        dir(env.WORKSPACE){
                                            catchError(buildResult:'FAILURE', stageResult:'FAILURE'){
                                                if(Environment.equalsIgnoreCase("")) {
                                                   ])
                                                    {
                                                        sh "echo Running the build in '${Environment}' environment"
                                                        sh "mvn clean test -DBrowserType=browserstack_'${exebrowser}' -DsuiteXmlFile=testng.xml -DprojName=ABC -DPlatform_password=$PASSWORD -DGroupToRun='${GroupsToRun}' -DAutomate_key=$Automate_key -DMFA_secret=$mfa_secret -DMFA_recover_code=$mfa_recovery -Demail_passcode=$EmailAuthPasscode -DEnvironment=$Environment -DRetry_Count=$Retry_Count -DClientSecret=$ClientSecret"
                                                    }
                                                } else {
                                                    withCredentials([string(credentialsId: 'automationPassword-Admin', variable: 'PASSWORD'), string(credentialsId:'browser_stack_automation_key', variable: 'Automate_key'),  string(credentialsId:'mfa_secrect_key', variable: 'mfa_secret'), string(credentialsId:'mfa_recovery_code', variable: 'mfa_recovery'), string(credentialsId:'cancelCallback-AuthToken', variable: 'AuthToken')]) {
                                                        sh "echo Running the build in '${Environment}' environment"
                                                        sh "mvn clean test -DBrowserType=browserstack_'${exebrowser}' -DsuiteXmlFile=testng.xml -DprojName=ABC -DPlatform_password=$PASSWORD -DGroupToRun='${GroupsToRun}' -DAutomate_key=$Automate_key -DMFA_secret=$mfa_secret -DMFA_recover_code=$mfa_recovery -DEnvironment=$Environment -DRetry_Count=$Retry_Count -DAuthToken=$AuthToken"
                                                    }

                                            }

                                            if((params.AXE && GroupsSelectedSize >= 1) || (params.RunEntireSuite && GroupsSelectedSize == 1)){
                                                sh "npm i -D axe-html-reporter"
                                                if("${exebrowser}".contains('chrome')){
                                                    sh "node AxeHTMLReport.js"
                                                }
                                                else{
                                                    echo "Skipping Axe reports on non chrome browsers"
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

pipeline {
    agent {
        label 'java'
    }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['compile', 'package', 'clean package'], description: 'This is MAVEN_GOAL Pick one Option') 
    }
    triggers {
        pollSCM('*/10 * * * 0-6')
    }
    stages {
        stage('git clone') {
            steps {
                git url: 'https://github.com/maurjadhav/spring-petclinic-jenkins.git',
                    branch: 'main'
            }
        }
        stage('build') {
            steps {
                mail bcc: '', body: 'Build started', cc: '', from: '', replyTo: '',
                    subject: "Build started for ${JOB_BASE_NAME} with Build Id ${BUILD_ID}", to: 'all@learnigthoughts.io'

                sh "mvn ${params.MAVEN_GOAL}"
                junit testResults: '**/surefire-reports/*.xml'
                archive 'target/spring-petclinic-*.jar'

                mail bcc: '', body: 'Build completed', cc: '', from: '', replyTo: '',
                    subject: "Build completed for ${JOB_BASE_NAME} with Build Id ${BUILD_ID}", to: 'all@learnigthoughts.io'
            }
            post {
                failure {
                    mail bcc: 'all@learningthoughts.io',
                        from: 'jenkins@learningthouths.io',
                        to: "dev@learningthoughs.io",
                        subject: "Build of ${JOB_BASE_NAME} with Build Id ${BUILD_ID} is failed",
                        body: "Refer to ${RUN_DISPLAY_URL} for more info"
                }
//                success {
//                    mail bcc: 'all@learningthoughts.io',
//                        from: 'jenkins@learningthouths.io',
//                        to: "dev@learningthoughs.io",
//                        subject: "Build of ${JOB_BASE_NAME} with Build Id ${BUILD_ID} is success",
//                        body: "Refer to ${RUN_DISPLAY_URL} for more info"
//                }
            }
        }
    }
}
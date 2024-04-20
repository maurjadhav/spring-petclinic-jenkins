pipeline {
    agent {
        label 'java'
    }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['compile', 'package', 'clean package'], description: 'This is MAVEN_GOAL Pick one Opetion') 
    }
    triggers {
        pollSCM('* * * * *')
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
                sh "mvn ${params.MAVEN_GOAL}"
                junit testResults: '**/surefire-reports/*.xml'
                archive 'target/spring-petclinic-*.jar'
                mail bcc: '', body: 'Build completed', cc: '', from: '', replyTo: '',
                subject: 'Build completed', to: 'all@learnigthoughts.io'
            }
        }

    }
}
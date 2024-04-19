pipeline {
    agent {
        label 'java'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/maurjadhav/spring-petclinic-jenkins.git',
                    branch: 'main'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'

            }
        }

    }
}
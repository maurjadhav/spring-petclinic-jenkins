pipeline {
    agent {
        label 'java'
    }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['compile', 'package', 'clean package'], description: 'Pick something') 
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
                sh 'mvn ${params.MAven_GOAL}'

            }
        }

    }
}
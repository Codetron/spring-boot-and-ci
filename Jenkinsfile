pipeline {
    agent any

    tools {
        jdk 'JDK 21'
    }

    stages {
        stage('checkout SCM') {
            steps {
                echo 'Checking out..'
                checkout scmGit(branches: [[name: '*/develop'], [name: '*/main'], [name: '*/pr-*']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_account_token', url: 'https://github.com/Codetron/spring-boot-and-ci.git']])
            }
        }
        stage('Build') {
            steps {
                echo 'Testing..'
                dir('simple-spring-boot') {
                    sh 'mvn package'
                }
            }
        }
/*         stage('Build image') {
            steps {
                echo 'Deploying....'
                dir('simple-spring-boot') {

                }
            }
        } */
    }
}
pipeline {
    agent any
    tools{
    maven 'maven3.8.7'    
    }

    stages {
        stage('clone the repository') {
            steps {
             git 'https://github.com/azurebose/javademoprjct.git'
            }
        }
        stage('build') {
            steps {
             sh 'mvn clean install'
            }
        }
        stage('deploy to tomcat') {
            steps {
             deploy adapters: [tomcat8(credentialsId: 'admin', path: '', url: 'http://44.211.226.43:8080')], contextPath: 'smaple-webapplication', war: '**/*.war'
            }
        }
    }
}

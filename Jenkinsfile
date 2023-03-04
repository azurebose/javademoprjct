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
             deploy adapters: [tomcat8(credentialsId: 'admin', path: '', url: 'http://3.86.234.162:8080')], contextPath: 'smaple-webapplication', war: '**/*.war'
            }
        }
    }
}

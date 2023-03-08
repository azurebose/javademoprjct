pipeline {
    agent any
    tools{
    maven 'maven 3.8.7'    
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
        stage('Build Docker Image') {
            steps {
                sh '''
              docker build . --tag web-application:$BUILD_NUMBER
              docker tag web-application:$BUILD_NUMBER  474648476402.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
                
                '''
                
            }
        }  
      
   stage('Push Docker Image') {
steps{
 withAWS(credentials: 'f3802823-8002-4bcc-8680-7d298abe1f9c', region: 'us-east-1') {
       
                    sh '''
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 108290765801.dkr.ecr.us-east-1.amazonaws.com
                   docker push 108290765801.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
                    '''
                }
            } 

        }
            
      }
    }

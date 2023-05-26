pipeline {
    agent any
    stages {
         stage('Clean WS, Checkout adn Build Project') {
            cleanWs()
            scmInfo = checkout scm
             dir( "Medicare/Medicare-Backend" ) {                              
                  withEnv(["PATH=${jdk}/bin:$PATH"]) {
                        sh "java -version"
                        withMaven {
                                sh "mvn clean install"
                                sh "mvn package"
                                }
                        }
                        archiveArtifacts 'Medicare-Backend/target/surefire-reports/*.xml'
                        junit 'userip-rest-service/target/surefire-reports/*.xml'
            }
        }
        stage('docker run') {
              dir( "Medicare/Medicare-Backend" ) {    
                steps {
                    sh "docker compose build" 
                    sh "docker compose up" 
                }  
            }
              dir( "Medicare/Medicare-Frontend" ) {    
                steps {
                    sh "docker compose build" 
                    sh "docker compose up" 
                }  
            }
        }
    }
}

pipeline {
  agent any

  tools {
    jdk 'java11'
    maven 'maven3.6.3'
  }
  
  environment {

      sonar_url = 'http://172.31.93.142:9000'
      sonar_username = 'admin'
      sonar_password = 'admin'
      nexus_url = '172.31.93.142:8081'
      artifact_version = '4.0.0'

 }
/* parameters {
      string(defaultValue: 'main', description: 'Please type any branch name to deploy', name: 'Branch')
 } */

stages {
   /* stage('Git checkout'){
      steps {
        git branch: '${Branch}',
        url: 'https://github.com/chinni4321/helloworld.git'
      }
    }*/
    stage('Maven build'){
      steps {
        sh 'mvn clean install'
      }
    }
  stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('sonarqube') {
           sh '''
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" -Dsonar.sourceEncoding=UTF-8
           '''
           }
         }
      } 
 }
}

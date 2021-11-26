pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }

    stages {
        stage('gitcheckout') {
            steps {
               git branch: 'main', credentialsId: 'discc', url: 'https://github.com/mamathamamidala/WebAppExample.git' 
          }
       }
         stage('build') {
             steps {
              bat 'mvn clean install'  
        }
      }
      stage('codequality') {
             steps {
               bat 'mvn sonar:sonar'
        }
      }
      stage('deploy') {
             steps {
              deploy adapters: [tomcat8(credentialsId: 'tomacat.cred', path: '', url: 'http://localhost:7000/')], contextPath: 'WebAppExample', war: '**/*.war'
        }
      } 
   }
 }
 

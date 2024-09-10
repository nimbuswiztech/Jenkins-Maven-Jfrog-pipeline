pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    stages{
       stage('GetCode'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/nimbuswiztech/maven_webapp.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarserver') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
                }
            }
        }
       
    }
}

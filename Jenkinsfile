pipeline{
        agent {
                docker {
                image 'maven'
                args '-v $HOME/.m2:/root/.m2'
                //args '-u root'
                }
        }
        stages{
              stage('Sonar Scan'){
                  steps{
                      script{
                      withSonarQubeEnv('sonarserver') { 
                      sh "mvn sonar:sonar"
                       }
		              // sh "mvn clean install"
                  }
                }  
              }
              stage('Maven Build'){
                  steps{
                      script{
		                  sh "mvn clean install"
                  }
                }  
              }
              stage('Deploy'){
                  steps{
                    deploy adapters: [tomcat8(credentialsId: 'Tomcat-admin', path: '', url: 'http://3.86.240.168:8080/')], contextPath: 'demo', war: 'target/*.war'
                }  
              }
        }
}

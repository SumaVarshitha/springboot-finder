pipeline {
    agent any
   
   
    stages {
		 
        stage('build') {
            
		   agent {
			   docker { image 'sumavarshitha/java-maven-node' }}
		steps {
			sh 'rm -rf springboot-finder' 
	        sh 'git clone https://github.com/SumaVarshitha/springboot-finder.git'
                sh "mvn clean package"
            
	    }
        }
        stage('SonarQube Analysis'){
		 environment{
               scannerHome = tool 'sonars'
                   }
            steps{
               withSonarQubeEnv('sonar'){
                    //sh '${sonarscanner}/bin/sonar-scanner -Dproject.settings=./sonar-project.properties'
		       sh "${scannerHome}/bin/sonar-scanner"
               //sh 'mvn sonr:sonar' 
	       }
            }
        }

    
        
       stage("Quality Gate") {
            steps {
              timeout(time: 3, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
        }
    }
       
}

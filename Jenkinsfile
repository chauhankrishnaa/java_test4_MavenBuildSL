pipeline {
	agent any
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			 sh 'mvn -B -DskipTests clean package'
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	
	stage('deployment'){
		steps{
		deploy adapters: [tomcat9(url: 'http://10.150.17.37:8080/', 
                              credentialsId: 'tomcat_credentials')], 
                     war: 'target/*.war',
                     contextPath: 'java-example'
		}
		
	}
	
	stage('Notification'){
		steps{
		emailext(
			subject: "Job Completed",
			body: "Jenkins pipeline job for maven build job completed",
			to: "krishna.chauhan@acuteinformatics.in"
		)
		}
	}
	}
}

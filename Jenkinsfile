pipeline {
	agent any
	stages {
		stage("Cleaning stage") {
			steps {
				
			     bat "mvn clean"
			}

		}
		stage("Testing stage") {
			steps {		
			     bat "mvn test"
		        }
		}
		stage("Packaging stage"){
		       steps {
			     bat "mvn package"
		       }
				
			}
		stage("Consolidate Results") {
			steps {
				input ("Do you want to capture results?")
				junit '**/target/surefire-reports/TEST-*.xml'
				archive 'target/*.jar'
			}
		}
		stage("Email Build Status"){
			steps {
				mail body: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult} \n\nCheck console output at ${env.BUILD_URL} to view the results.", subject: "${env.JOB_NAME}  - Build # ${env.BUILD_NUMBER}  - ${currentBuild.currentResult}!!", to: 'gnanadurga@gmail.com'
			}
		}
	}
}

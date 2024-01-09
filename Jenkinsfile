pipeline {

	agent any

	tools {

		maven 'MAVEN3'
		jdk 'Oracle8'

	}

	stages {


		stage('Fetch code') {

			steps{

				git branch: 'master' , url: 'https://github.com/jenkins-docs/simple-java-maven-app.git' 
			}

			

		}

		stage('code test') {

			steps {

				sh 'mvn test'

			}
			
		}

		stage('code analysis with checkstyle') {

			steps {

				sh 'mvn checkstyle:checkstyle'

			}

			post {

				success {

					echo 'Generated analysis result'
				}

			}

		}

		stage('Build package') {
	      steps {
	         sh 'mvn clean install'
	      }
	    }


		stage('upload to nexus') {

			 steps {

	          nexusArtifactUploader(
                nexusVersion: 'nexus3',
		        protocol: 'http',
		        nexusUrl: '3.222.188.140:8081',
		        groupId: 'QA1',
		        version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
		        repository: 'TestQA2',
		        credentialsId: 'NexusLogin',
		        artifacts: [
		            [artifactId: 'vproapp',
		             classifier: '',
		             file: 'target/my-app-1.0-SNAPSHOT.jar',
		             type: 'jar']
        ]
     )


	      }


		}



	}

}

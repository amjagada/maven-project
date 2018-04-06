pipeline{
	agent { label 'slave1' }

	stages{
		stage('Build'){
			steps{
				sh '/deploy/tools/maven/bin/mvn clean package'
			}
			post{
				success{
				echo 'Now Archive]ing...'
				sh 'ls -ltr'
				archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}

		stage('Deploy to Staging'){
			steps{
				build job: 'Udemy/deploy-to-staging'
			}
		}
	}
}
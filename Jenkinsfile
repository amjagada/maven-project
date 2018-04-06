pipeline{
	agent { label '!master' }

	stages{
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
			post{
				success{
				echo 'Now Archiveing...'
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

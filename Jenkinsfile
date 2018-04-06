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
		stage('Deploy to Production'){
			steps{
				timeout(time:5, unit:'DAYS'){
					input messege: 'Approve production deployment?'
				}
				build job: 'Udemy/deploy-to-production'
			}
			post{
				success{
					echo 'Code deployed to production.'
				}
				failure{
					echo 'Deployment failed'
				}
			}
		}
	}
}

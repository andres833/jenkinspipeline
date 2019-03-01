pipeline {
    agent any
    stages{

        stage ('Build'){
            steps {
                sh 'mvn clean package'
            }
	    post {
	        success {
		    echo 'Now Archiving...'
		    archiving artifacts: '**/target/*.war'
            }
        }
    }
        stage ('Deploy to Staging'){
            steps {
                build job: 'deploy-to-staging-PAC'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-to-Prod-PAC'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }
    }
}

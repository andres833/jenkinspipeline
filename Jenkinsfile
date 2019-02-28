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
                build job: 'Deploy-to-staging'
            }
        }
    }
}

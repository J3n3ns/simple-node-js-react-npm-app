pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    environment {
        CI = 'true' 
    }
    stages {
        stage('Build2') { 
            steps {
                sh 'npm install' 
            }
        }
    
    stage('Test2') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
    stage('OWASP Dependency Check') {
	    steps {
		dependencyCheck additionalArguments: '', odcInstallation: 'default'
            }
        } 
    stage('Deliver'){
		steps {
			sh './jenkins/scripts/test.sh'
            }
        }
    }
}

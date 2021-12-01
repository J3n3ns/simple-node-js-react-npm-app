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
		dependencyCheck additionalArguments: '--disableAssembly --enableExperimental --format HTML --format XML', odcInstallation: 'Default'
            }
    } 
    stage('Deliver2') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                #input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

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
		dependencyCheck additionalArguments: '--disableAssembly --enableExperimental --format HTML --format XML', odcInstallation: 'OWASP'
            }
        } 
    stage('Deliver'){
		steps {
			sh './jenkins/scripts/test.sh'
		}
	}
    }
    post {
		success {
			dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
		}
	}
}


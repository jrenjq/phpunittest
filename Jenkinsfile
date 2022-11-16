pipeline {
	agent {
		docker {
			image 'composer:latest'
		}
	}
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/jrenjq/JenkinsDependencyCheckTest.git'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'Default'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
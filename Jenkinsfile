pipeline {
	agent any
	stages {
		stage('Build') {
			agent {
				docker {
					image 'composer:latest'
				}
			}
			steps {
				sh 'composer install'
			}
		}
		stage('Test') {
			agent {
				docker {
					image 'composer:latest'
				}
			}
			steps {
                sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            }
		}
		stage('OWASP DependencyCheck') {
			agent any
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
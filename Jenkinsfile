pipeline {
    agent {
        docker {
            image 'node:20.9.0-alpine3.18' 
            args '-p 3000:3000' 
        }
    }
    stages 
		stage('Test') {
            steps {
				sh 'chmod +x ./jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
		stage('OWASP Dependency-Check Vulnerabilities') {
            agent any
            steps {
                script {
                    dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
            }
        }
		stage('Deliver') {
            steps {
				sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/deliver.sh'
            }
        }
		stage('Ending') {
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
				sh 'chmod +x ./jenkins/scripts/kill.sh'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
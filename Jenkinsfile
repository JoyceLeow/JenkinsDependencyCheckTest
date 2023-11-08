pipeline {
    agent {
        docker {
            image 'node:20.9.0-alpine3.18' 
            args '-p 3000:3000' 
        }
    }
    stages {
			stage('OWASP Dependency-Check Vulnerabilities') {
      steps {
        dependencyCheck additionalArguments: '--format HTML, odcInstallation: 'OWASP Dependency-Check Vulnerabilities'

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
}	
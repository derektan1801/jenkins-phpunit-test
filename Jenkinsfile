pipeline {
	agent {
		docker { image 'maven' }
	}
	stages {
		stage ('Checkout') {
			steps {
				git branch:'main', url: 'https://github.com/derektan1801/jenkins-phpunit-test.git'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv() {
						sh "${tool("SonarQube")}/bin/sonar-scanner \
						-Dsonar.projectKey=OWSAP \
						-Dsonar.sources=. \
						-Dsonar.host.url=http://192.168.163.136:9000 \
						-Dsonar.login=60070b3f5f5e07e30fea698d91985bc963788c49"
						}
					}
				}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}

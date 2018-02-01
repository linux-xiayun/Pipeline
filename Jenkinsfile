pipeline {
    agent none
    stages {
        stage('Maven Build') {
            agent { docker 'maven:3-alpine' }
			options { 
				    retry(3)
					timeout(time: 10, unit: 'MINUTES')
					}
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
		stage('Example') {
		    input {
		        message "Should we continue?"
			    ok "Yes, we should."

				parameters {
				    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
				}
		    }
			steps {
			    echo "Hello, ${PERSON}, nice to meet you."
			}
		}
        stage('Java Build') {
            agent { docker 'openjdk:8-jre' }
			options { 
				    retry(3)
					timeout(time: 10, unit: 'MINUTES')
					}
            steps {
                echo 'Hello, JDK'
                sh 'java -version'
            }
        }
    }
	post {
	    success {
		    echo "Well Done!"
		}
		failure {
		    echo "sorry failed!"
		}
		unstable {
		    echo "en...unstable!"
		}
		
	}
}
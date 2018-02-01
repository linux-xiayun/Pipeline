pipeline {
    agent none
	parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    }
	
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
		stage('Aborted') {
		    input {
		        message "Should we continue?"
			    ok "Yes, we should."

				parameters {
				    string(name: 'PERSON', defaultValue: 'Mr XiaYun', description: 'Who should I say hello to?')
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
		stage('Finished'){
		    steps {
			    echo "Hello ${params.PERSON}"
			}
		}
		parallel {
		    stage('Branch A') {
			    steps { echo "On Branch A" }
			}
			stage('Branch B') {
			    steps { echo "On Branch B" }
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
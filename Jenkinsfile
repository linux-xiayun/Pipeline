pipeline {
    agent none
    stages {
        stage('Maven Build') {
            agent { docker 'maven:3-alpine' }
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
        stage('Java Build') {
            agent { docker 'openjdk:8-jre' }
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
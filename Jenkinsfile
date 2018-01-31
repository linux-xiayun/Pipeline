pipeline {
    agent { dokcer 'maven:3-alpine' }
	stages('Example Build') {
	    steps {
		    sh 'mvn -B clean verify'
        }
    }
}
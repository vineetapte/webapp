pipeline {
    agent any
    tools { 
        maven 'maven' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
	}
	    stage ('Build') {
		    steps {
			sh 'mvn clean package'
		    }
	    }
	    stage ('Deploy-to-Tomcat'){
		    steps {
			    sshagent(['tomcat']) {
				    sh "scp -o StrictHostKeyChecking=no target/WebApp.war vineet@192.168.0.108:/var/lib/tomcat9/webapps/WebApp.war"
			    }
		    }
	    }
    }
}

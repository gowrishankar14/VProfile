pipeline {
    agent any

	tools {
		jdk  'JDK11'
	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    steps {
	        checkout scm
	    }
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Deployment') {
            steps {
                sh 'sshpass -p "welcome" scp target/gamutgurus.war ec2-user@54.221.74.52:/root/apache-tomcat-8.5.84/webapps'
                sh 'sshpass -p "welcome" ssh ec2-user@54.221.74.52 "/root/apache-tomcat-8.5.84/bin/startup.sh"'
            }
        }
    }
}

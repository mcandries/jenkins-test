// Powered by Infostretch 

timestamps {

node () {

	stage ('Test1 - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'jenkin_test', url: 'https://github.com/mcandries/jenkins-test']]]) 
	}
	stage ('Test1 - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		} 
	}

	stage ('Test1 - Quality Analysis') {
		withMaven(maven: 'maven') { 
				if(isUnix()) {
					sh "mvn sonar:sonar" 
				} else { 
					bat "mvn sonar:sonar" 
				} 
			} 
	}


	stage ('Test1 - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'mcandries@outlook.com', sendToIndividuals: false])
 
	}
}
}
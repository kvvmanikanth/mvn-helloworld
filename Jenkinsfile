pipeline {



agent any

//agent {label 'linux'} if you want to run this project in jenkins slave,before that you have to configure jenkins slave node
       

       tools {

	//WE HAVE DEFINED THE VALUES OF JAVA_HOME & m2_HOME IN GLOBAL TOOL CONFIGURATION

        jdk 'JAVA_HOME'
        maven 'M2_HOME'      
       }


      triggers {
         cron('* * * * *')
            }



stages {



       stage('GitClone') {
            steps {
                git 'https://github.com/kvvmanikanth/mvn-helloworld.git'
                  }
            }



       stage('MavenBuild') {
              steps {
                  sh "mvn --version"
                  sh "mvn clean install"
              }
       }



      stage('Publish') {
             steps {

		//we installed nexus artifactoryplugin, then checkin snipet generator for nexus,enter the details & click on
                   snippet generator


                nexusArtifactUploader artifacts: [
			              [artifactId: 'mvn-hello-world', 
				      classifier: '', 
				      file: '/var/lib/jenkins/workspace/Demo_Pipeline/target/my-app.jar', 
				      type: 'jar']], 
			              credentialsId: 'c2939100-37d8-478d-9f22-0e45267e7333', 
			              groupId: 'com.mycompany.app',
			              nexusUrl: 'host123.com:8081',
			              nexusVersion: 'nexus3', 
			              protocol: 'http', 
			              repository: 'sample1', 
			              version: '1.0-SNAPSHOT'
			}
      } 
}
}

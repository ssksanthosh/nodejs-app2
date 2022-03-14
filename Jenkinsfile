pipeline
{
  environment {
    registry = "ssksanthosh/ex-nodejs-app2"
    registryCreds = 'dockerhub'
    dockerCreds = credentials('dockerhub')
    dockerImage = ''
  }
 agent any
 	stages {
 		stage ('checkout code'){
 			steps {
 				     echo "checking out code"
 				     cleanWs()
             git branch: 'main', url: 'https://github.com/ssksanthosh/nodejs-app2.git'
 				     //checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ssksanthosh/nodejs-app2.git']]])
 		       	}
          }
 		stage ('docker build') {
 			steps {
 				echo "building docker image"
        script {
          dockerImage = docker.build registry
        }
       }

 				//sh 'docker build -t ssksanthosh/ex-nodejs-app2 .'
 		}
 	    stage ('upload docker image') {
 	    	steps {
 	    		script {
          docker.withRegistry( '', registryCreds ) {
          dockerImage.push()
          }
        }
 	     }
 		}
 	}
}

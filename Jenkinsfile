pipeline{

   agent any

	//create dockerhub credential in github with your dockerhub Username and Password/Token
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git 'https://github.com/febfun1/DevOpsClassCodes1.git'
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t febfun/private:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username febfun --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push febfun/private:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}

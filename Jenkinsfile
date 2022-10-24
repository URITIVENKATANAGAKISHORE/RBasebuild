pipeline{
	agent any
	stages{
		stage('Git Check Out') {
			git credentialsId: 'github', url: 'https://github.com/URITIVENKATANAGAKISHORE/RBasebuild.git'
			echo 'Git Checkout Completed'
		}
		stage('Build Docker Image'){
			steps{
				sh 'sudo docker build -t vaultrotation.azurecr.io/Rbase:$BUILD_NUMBER .'
				echo 'Build Image completed'
			}
		}
		stage('Login to Azure and push the docker images to acr hub'){
			steps{
				withCredentials(){
					sh 'docker login -u ${username} -p ${password} 
					sh 'docker image push :${BUILD_NUMBER}'
				}
			}
		}
		stage('Login to Docker Hub') {      	
			steps{                       	
			sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                		
			echo 'Login Completed'      
			}           
		}		
	}
}

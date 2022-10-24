pipeline {
	agent any
		environment {
			//once you create ACR in Azure cloud, use that here
			registryName = "vaultrotation"
			//- update your credentials ID after creating credentials for connecting to ACR
			registryCredential = 'ACR'
			dockerImage = ''
			registryUrl = 'vaultrotation.azurecr.io'
		}
    
    stages {
		stage ('checkout') {
            steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/URITIVENKATANAGAKISHORE/RBasebuild.git']]])
            }
        }
		stage ('Build Docker image') {
            steps {
                
                script {
                    dockerImage = docker.build registryName
                }
            }
        }
       
		stage('Upload Image to ACR') {
			steps{   
				script {
					docker.withRegistry( "http://${registryUrl}", registryCredential ) {
					dockerImage.push()
				}
			}
		}
	}
}

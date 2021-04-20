pipeline {
    agent any
 
    tools {nodejs "node"}
    
    environment {
        registry = "maidercalzada/node-api-hello-world"
        registryCredential = '44b49d1c-17e9-467a-b38f-908d527c6697'
        docker_image_name = "nodeapi"
    }
 
    stages {
 
        stage('Cloning Git') {
            steps {
                git 'https://github.com/MaiderC/Node-js-hello-world-API-CI.git'
            }
        }
        
        stage('Build image') 
        {
          steps
          {
            script 
            {
                docker.withRegistry('', registryCredential)
                {
                  dockerImage = docker.build docker_image_name + ":$BUILD_NUMBER"
                }
            }
          }
        }
        
       stage('Deploy image') {
          steps{
            script {
              docker.withRegistry('', registryCredential) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push("latest")
              }
            }
          }
        }
        
    }
}
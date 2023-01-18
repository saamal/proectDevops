
pipeline {
    agent any
    environment{
     
        manifestsimg= ''
        registry="https://hub.docker.com/repositories/amalsg"
        credentialregistry = "amalsg"
           }
       // code checkout
       stages {
           stage('code Checkout') {
            steps {
             git url: 'https://github.com/microservices-demo/carts.git'
                   }
           }
  
           // Building Docker images
        stage('Building docker images') {
           steps{
             script {          
              manifestsimg=docker.build("manifests-image","/home/azureuser/microservices-demo/deploy/kubernetes")
            }
           }
        }
        //Uploading Docker images into docker hub
       stage('Uploading to docker hub') {
         steps{
         script {
           docker.withRegistry(registry, credentialregistry){
                manifestsimg.push('latest')
           }
           }
            }
        }    
         stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
       
    }
}
   

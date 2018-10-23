pipeline {
     agent any



environment {
        
          IMAGE = 'testimage'
          DOCKER_REGISTRY = 'hub.docker.com'
          REGISTRY_CREDENTIAL = '617ee2e4-6f49-483e-9520-96e8c9e2752c'
      }


   stages {

       stage('checkout') {
        steps {
          checkout scm
        }
      }


   stage('build docker image') {
         steps {
            script {
               dockerImage = docker.build("ayodejiemiloju1/${IMAGE}:${env.BUILD_NUMBER}")

         }
       }
      }


    stage('push  to docker registry') {
         steps {
             script {
                withDockerRegistry(credentialsId: "${REGISTRY_CREDENTIAL}", url: '') {
                 dockerImage.push("${env.BUILD_NUMBER}")
                 dockerImage.push("latest")
               }
           }
         }
        }

 }
}

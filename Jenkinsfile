pipeline {
     agent any



environment {
       IMAGE = "testimage"
       DOCKER_REGISTRY = "https://hub.docker.com"
       REGISTRY_CREDENTIAL = "6b92377a-afe8-4263-88c4-42f36315d5b4"
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

                docker.withRegistry(DOCKER_REGISTRY, REGISTRY_CREDENTIAL) {
                 dockerImage.push("${env.BUILD_NUMBER}")
                 dockerImage.push("latest")
               }
           }
         }
        }

 }
}
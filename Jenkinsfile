pipeline {
     agent any



environment {
       PATH = "/Users/gskdevops/.fastlane/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
       IMAGE = "testimage"
       DOCKER_REGISTRY = "https://hub.docker.com"
       REGISTRY_CREDENTIAL = "https://osbsolutions-keysvault.vault.azure.net/secrets/ayodejiemiloju1"
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

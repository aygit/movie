pipeline {
     agent any



environment {
       PATH = "/Users/gskdevops/.fastlane/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
       IMAGE = "testimage"
       DOCKER_REGISTRY = "https://hub.docker.com"
       REGISTRY_CREDENTIAL = "5a2d152f-f848-4801-8110-219493beba83"
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

                docker.withRegistry(DOCKER_REGISTRY, 6b92377a-afe8-4263-88c4-42f36315d5b4) {
                 dockerImage.push("${env.BUILD_NUMBER}")
                 dockerImage.push("latest")
               }
           }
         }
        }

 }
}

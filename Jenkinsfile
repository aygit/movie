pipeline {
     agent any



environment {
         pom = 'https://registry.hub.docker.com'
          IMAGE = 'testimage'
          DOCKER_REGISTRY = 'registry.hub.docker.com'
          REGISTRY_CREDENTIAL = '617ee2e4-6f49-483e-9520-96e8c9e2752c'
      }



     triggers {
        pollSCM '* * * 3 *'
   }

   stages {

       stage('checkout') {
        steps {
          git branch: 'master', url: 'git@github.com:aygit/movie.git'
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
               withDockerRegistry(credentialsId: "${REGISTRY_CREDENTIAL}", url: "https://${DOCKER_REGISTRY}") {
                dockerImage.push("${env.BUILD_NUMBER}")
                dockerImage.push("latest")
               }
           }
         }
        }


     stage('docker logout') {
       steps {
          script {
          docker logout "https://${DOCKER_REGISTRY}"
          }
       }

     }


    stage('clean up') {
     steps {

        sh "docker rmi ${DOCKER_REGISTRY}/${IMAGE}:${env.BUILD_NUMBER}"
         sh "docker rmi ${DOCKER_REGISTRY}/${IMAGE}:latest"
         }
       }
 }
}

pipeline {
     agent any

// check new code

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

  
   stage('build docker image uat') {
        when {
            branch 'uat'
           }
 
         steps {
            script {
               dockerImage = docker.build("ayodejiemiloju1/${IMAGE}:${env.BUILD_NUMBER}")

         }
       }
      }



     stage('login to the registry') {
     steps {
    withCredentials([
      [
        $class: 'UsernamePasswordMultiBinding',
        credentialsId: '617ee2e4-6f49-483e-9520-96e8c9e2752c',
        usernameVariable: 'DOCKERUSER',
        passwordVariable: 'DOCKERPASS'
      ]
    ]) {
      echo 'Logging into DockerHub'
      sh '''#! /bin/bash
         echo $DOCKERPASS | docker login -u $DOCKERUSER --password-stdin
         '''

     }
    }
  }

    stage('push  to docker registry') {
         steps {
             script {

                 dockerImage.push("${env.BUILD_NUMBER}")
                 dockerImage.push("latest")
               }
           }
         }
        }



 }

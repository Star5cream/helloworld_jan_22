pipeline {

   agent any

   tools{

       maven 'Maven88'

   }

   environment {

       registry = '654654519835.dkr.ecr.us-east-1.amazonaws.com/devops_repository'

       registryCredential = 'jenkins-ecr'

       dockerimage = ''

   }

   stages {

       stage('Checkout'){

           steps{

               git branch: 'main', url: 'https://github.com/Star5cream/helloworld_jan_22.git'

           }

       }

       stage('Code Build') {

           steps {

               sh 'mvn clean package'

           }

       }

       stage('Test') {

           steps {

               sh 'mvn test'

           }

       }

       stage('Build Image') {

           steps {

               script{

                   dockerImage = docker.build registry + ":$BUILD_NUMBER"

               } 

           }

       }

       stage('Deploy image') {

           steps{

               script{ 

                   docker.withRegistry("https://"+registry,"ecr:us-east-1:"+registryCredential) {

                       dockerImage.push()

                   }

               }

           }

       }  

   }

}


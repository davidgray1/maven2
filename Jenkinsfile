pipeline {

    agent none 
    stages {

        stage('Complile') {

    agent {

       docker {

         image 'maven:3-alpine'

       }
    }
            steps {

                sh 'mvn clean compile'
                sh 'ls -l'
            }
        }
        

stage('Test') {


    agent {


       docker {
         image 'maven:3-alpine'
       }
    }
            steps {
                sh 'mvn package'
                sh 'ls -l'
            }
        }

stage('Docker') {

            agent {

              docker {

                 image 'docker:latest'

              }

            }
            steps {
                sh 'docker build -t in-jenkins-image .'
                sh 'ls -l'
            }
        }

stage('Deploy') {

    agent {


       docker {
         image 'maven:3-alpine'
       }
    }
            steps {
                sh 'mvn install'
                sh 'ls -l'
            }
        }
    }

post {

                 



          failure {

             echo 'Build failed'

           }
     }
}


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
stage('Push'){
	withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
	def registry_url = ""https://cloud.docker.com/repository/registry-1.docker.io/davidgray123/jenkinstodocker
	bat "docker login -u $USER -p $PASSWORD ${https://cloud.docker.com/repository/registry-1.docker.io/davidgray123/jenkinstodocker}"
	docker.withRegistry("http://${https://cloud.docker.com/repository/registry-1.docker.io/davidgray123/jenkinstodocker}", "docker-hub-credentials"){
	
	bat "docker push in-jenkins-image:latest"
				}





    }

post {

	  success {
             archiveArtifacts(artifacts: '**/target/*.jar', allowEmptyArchive: true)   
           }                 



          failure {

             echo 'Build failed'

           }
     }
}


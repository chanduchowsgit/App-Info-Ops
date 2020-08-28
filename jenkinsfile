
pipeline {
    
   agent any

   tools {
      maven "maven"
      ant "ant"
   }

   stages {
      stage('SCM') {
         steps {
            git 'https://github.com/chanduchowsgit/App-Info-Ops.git'
         }
      }
      stage('build') {
         steps {
            sh "mvn clean install"
         }
      }
      stage('artifact to s3') {
         steps {
            sh "ant upload-s3"
         }
      } 
      stage('docker-login') {
          steps {
            withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh "docker login -u $username -p $password"
            }
        }
    }
      stage('docker image') {
          steps{
              sh "ant docker-push all-clean"
         }
      }
    }
}

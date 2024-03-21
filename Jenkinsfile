pipeline {
  environment {
    imagename = "gopalgautam/assignment3"
    registryCredential = 'docker_registry_key_1'
    dockerImage = ''
  }
  agent {
    label 'docker' 
  }
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/Gopal-creater/practice.git', branch: 'main'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"
 
      }
    }
  }
}

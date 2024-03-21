pipeline {
  environment {
    imagename = "gopalgautam/assignment3"
    registryCredential = 'docker_registry_key_1'
    dockerImage = ''
  }
  agent any
  tools { //Allows you to define tools or installations needed for your pipeline.
    nodejs 'node' // 'node' should match the NodeJS installation name configured in Jenkins
    dockerTool 'docker'
  }
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/Gopal-creater/assignment3.git', branch: 'main'])
 
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
                    // Log in to Docker Hub
                    sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}"
                    
                    // Push the Docker image to Docker Hub
                    dockerImage.push()
        }
      }
    }
  }
}

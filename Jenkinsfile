pipeline {
  environment {
    imagename = "aakhil/testcase"
    registryCredential = 'jenkins-dockerhub-cred'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/akhiljosef/dockerbuild.git', branch: 'master'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
  }
}  
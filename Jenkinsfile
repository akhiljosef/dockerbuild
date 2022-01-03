pipeline {
  environment {
    imagename = "aakhil/testcase"
    DOCKERHUB_CREDENTIALS=credentials('jenkins-dockerhub-cred')
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
    stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push aakhil/testcase:latest'
			}
		}
	}
 post {
		always {
			sh 'docker logout'
		}
	}   
  
}  
pipeline {
  //https://medium.com/codex/how-to-push-a-docker-image-to-docker-hub-using-jenkins-487fb1fcbe25
  //https://faun.pub/docker-build-push-with-declarative-pipeline-in-jenkins-2f12c2e43807
  environment {
    imagename = "aakhil/testcase"
    DOCKERHUB_CREDENTIALS=credentials('jenkins-dockerhub-cred')
    dockerImage = ''
  }
  agent {
    node {
        label 'salve1'
    }
  }
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
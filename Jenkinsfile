pipeline {
    agent {
        node { label 'slave 3' }
	    
    } 
	        environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    stages {
        stage('Git clone') { 
            steps {
                git 'https://github.com/sanju6655/demo-java.git'
            }
        }

  stages {
    stage('Build') {
      steps {
        sh 'bin/build .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		def buildNumber = env.BUILD_NUMBER
		sh 'docker tag demo-java sreenivas123435/shreeni123:demo-java-${buildNumber}'
		
      }
    }
    stage('Push') {
      steps {
        sh 'docker push sreenivas123435/shreeni123:demo-java-${buildNumber}'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

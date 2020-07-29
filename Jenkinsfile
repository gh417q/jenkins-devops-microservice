// SCRIPTED
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

// DECLARATIVE
pipeline {
  agent any
  // agent { docker { image 'maven:3.6.3' } }
  environment {
	  mavenHome = tool "myMaven" // installed in Jenkins by this name
	  dockerHome = tool "myDocker" // installed in Jenkins by this name
	  PATH = "$PATH:$mavenHome/bin:$dockerHome/bin"
  }
  stages {
    stage('Build') {
      steps {
        echo "Build"
		sh 'mvn --version'
		sh 'docker version'
		echo "PATH: $PATH"
		echo "BUILD NUMBER: $env.BUILD_NUMBER"
		echo "BUILD ID: $env.BUILD_ID"
		echo "JOB NAME: $env.JOB_NAME"
		echo "BUILD TAG: $env.BUILD_TAG"
		echo "BUILD URL: $env.BUILD_URL"
	  }
    }
    stage('Test') {
      steps {
        echo "Test"
	  }
    }
    stage('Integration Test') {
      steps {
        echo "Integration Test"
	  }
    }
  }
  post {
	  always {
		  echo "running always"
	  }
	  success {
		  echo "running if success"
	  }
	  failure {
		  echo "running when failed"
	  }
	  unstable {
		  echo "build is unstable"
	  }
	  changed {
		  echo "build status changed"
	  }
  }
}
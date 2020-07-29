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
  // agent any
  agent { docker { image 'maven:3.6.3' } }
  stages {
    stage('Build') {
      steps {
        echo "Build"
		sh 'mvn --version'
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
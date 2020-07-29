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
    stage('Checkout') {
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
    stage('Complie') {
      steps {
        echo "Complie"
        sh 'mvn clean compile'
      }
    }
    stage('Test') {
      steps {
        echo "Test"
		sh 'mvn test'
	  }
    }
    stage('Integration Test') {
      steps {
        echo "Integration Test"
		sh 'mvn failsafe:integration-test failsafe:verify' // configured in pom.xml to run Cucumber Integration Tests
	  }
    }
	stage {
		steps {
			echo "Build jar"
			sh 'mvn package -DskipTests'
		}
	}

	stage('Build Docker Image') {
	  steps {
	    // docker build -t dh417q/currency-exchange-devops:$env.BUILD_TAG - plain call command
	    script {
	      dockerImage = docker.build("dh417q/currency-exchange-devops:${env.BUILD_TAG}")
	    }
	  }
	}
	stage('Push Docker Image') {
	  steps {
		script {
          docker.withRegistry('', 'dockerhub') {
            dockerImage.push();
		    dockerImage.push('latest');
		  }
		}
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
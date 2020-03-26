pipeline {
  agent none
  options {
    buildDiscarder(logRotator(numToKeepStr: '2')) //limits the log and and artifacts that are retained
    skipDefaultCheckout true //skips checking out the code by default in every stage
  }
  triggers {
    eventTrigger simpleMatch('hello-api-deploy-event')
  }
  stages {
    stage( 'Test' ) {
      agent { 
        kubernetes {
          label 'nodejs-app-pod2'
          yamlFile 'nodejs-pod.yaml'
        }
      }
      steps {
        checkout scm // clones and checkouts the code
        container('nodejs') {
          echo 'Hello World!'
          sh 'node --version'
        }
      }
    }
    stage('Build and Push Image') { // this will only run when a commit is made to the master branch
      when {
        beforeAgent true
        branch 'master'
      }
      steps {
        echo "TODO - build and push image"
      }
    }
    stage('Deploy') {
      when {
        beforeAgent true 
        beforeInput true //tells the when block to execute before the input is required so we only ask for input on master
        branch 'master'
      }
      options {
        timeout(time: 45, unit: 'SECONDS')
      }
      input {
        message "Should we continue?"
      }
      steps {
        echo "Continuing with Deployment"
      }
    }
  }
}

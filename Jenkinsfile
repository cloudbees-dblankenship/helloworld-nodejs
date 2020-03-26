pipeline {
  agent none
  options {
    buildDiscarder(logRotator(numToKeepStr: '2')) //limits the log and and artifacts that are retained
    skipDefaultCheckout true //skips checking out the code by default in every stage
  }
  stages {
    stage( 'Test' ) {
      agent { label 'nodejs-app' }
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
  }
}

pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '2'))
    skipDefaultCheckout true
  }
  stages {
    triggers {
    eventTrigger simpleMatch('hello-api-deploy-event')
    publishEvent simpleEvent('hello-api-deploy-event')  
  }
    stage('Test') {
      agent {
        kubernetes {
          label 'nodejs-app-pod-2'
          yamlFile 'nodejs-pod.yaml'
        }
      }
      steps {
        checkout scm
        container('nodejs') {
          echo 'Hello World!'   
          sh 'node --version'
        }
      }
    }
    stage('Build and Push Image') {
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

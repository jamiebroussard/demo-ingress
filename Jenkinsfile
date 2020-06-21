#!/usr/bin/groovy

@Library('jbroussard-shared') _  // Import Jenkins Global Library

pipeline {
  agent any
  environment {
    region          = "us-west-2"
    build_id        = "${BUILD_NUMBER}" // Jenkins build ID
    yamlfile        = "ingress.yaml"
  }
  // START THE PIPELINE
  stages {
    stage ('Deploy to Dev') {
      environment {
        cluster = "jbroussard-demo"
      }
      steps {
        script {
          // Setup kubectl
          aws.updateKubeConfig("$region", "$cluster")
          // apply
          //sh "kubectl apply -f sandbox_cluster_ingress.yml"
          sh "kubectl get svc"
        }
      }
    }
    stage ("Notify") {
      steps {
        script {
          utility.sendNotification()
        }
      }
    }
  }
}

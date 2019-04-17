pipeline {

 options {
  skipDefaultCheckout()
  buildDiscarder(logRotator(numToKeepStr: '20'))
 }
 agent any
 stages {
  stage('Tests') {
   steps {
    script {
     env.WORKSPACE = pwd()
     docker.image("gradle:5.4.0-jdk8-alpine").inside("-v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp") {
      sh "gradle test --info"
      sh "gradle compileIntegrationTestKotlin --info"
      sh "gradle integrationTest --info"
     }
    }
   }
  }
 }
}

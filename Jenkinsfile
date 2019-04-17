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
     docker.image("openjdk:8-jdk").inside("-v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp") {
      sh "gradle test --info"
      sh "gradle compileIntegrationTestKotlin --info"
      sh "gradle integrationTest --info"
     }
    }
   }
  }
 }
}

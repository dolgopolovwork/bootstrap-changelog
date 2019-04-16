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
     iC = docker.image("openjdk:8-jdk")
     iC.inside("-v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp") {
      sh "./gradlew test --info"
      sh "./gradlew compileIntegrationTestKotlin --info"
      sh "./gradlew integrationTest --info"
     }
    }
   }
  }
 }
}

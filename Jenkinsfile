pipeline {
  agent { label 'Jenkins-Agent' }
  tools  { 
    jdk 'Jdk17'
    maven 'Maven3'
  }
  stages {
    stage ("Cleanup Workspace"){
      steps {
        cleanWs()
      }
    }
    stage("Checkout from SCM"){
      steps{
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/AramEvin/registration-app'
      }
    }
    stage("Build Application") {
      steps{ 
        sh "mvn clean package"
      }
    }
    stage("Test Application") {
      steps{ 
        sh "mvn test"
      }
    }
    stage("SonarQube Analysis"){
      steps {
        script {
          withSonarQubeEnv(credentialsId: 'jenkins-sonarcude-token') {
            sh "mvn sonar:sonar"
          }
        }
      }
    }
    
  }
}

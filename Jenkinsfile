pipeline {
  agent { label 'Jenkins-Agent' }
  tools  { 
    jdk 'Jdk17'
    maven 'Maven3'
  }

  environment {
    APP_NAME = "register-app-pipline"
    RELEASE = "1.0.0"
    DOCKER_USER = "aramevinyan"
    DOCKER_PASS = 'dockerhub'
    IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
    IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
          withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
            sh "mvn sonar:sonar"
          }
        }
      }
    }
  }
}

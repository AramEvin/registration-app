pipeline {
  agent {label 'Jenkin-Agent' }
  tool  { 
    jdk 'Java-17'
    mavn 'Maven-3'
  }
  stages {
    stage ("Cleanup Workspace"){
      steps {
        cleanWs()
      }
    }
    stage("Checkout from SCM"){
      steps{
        git branch: 'main', crebdentialsId: 'GithubToken', url: 'https://github.com/AramEvin/registration-app.git'
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
  }
}

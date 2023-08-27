pipeline{
  agent any
  tools{
      maven 'maven3'
  }
  stages{
    stage("checkout"){
      steps{
        git 'https://github.com/jayaveeran13/my-app.git'
      }
    }
    stage("maven"){
      steps{
        sh "mvn clean package"
      }
    }
  }
}

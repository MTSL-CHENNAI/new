pipeline{
  agent any
  tools{
      tool name: 'maven3' type: 'maven
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

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
        sh "mv target/*war /target/myweb.war"
      }
    }
stage("tomcat") {
    steps {
        script {
            sshagent(['tomcat']) {
                // Copy the WAR file to the remote Tomcat webapps directory
                sh "scp -o StrictHostKeyChecking=no /target/myweb.war root@172.31.41.28:/opt/apache-tomcat-9.0.80/webapps/"

                // Remote commands to shutdown and startup Tomcat
                sh "ssh root@172.31.41.28 '/opt/apache-tomcat-9.0.80/bin/shutdown.sh'"
                sh "ssh root@172.31.41.28 '/opt/apache-tomcat-9.0.80/bin/startup.sh'"
            }
        }
    }
}








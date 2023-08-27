pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage("checkout") {
            steps {
                script {
                    git 'https://github.com/jayaveeran13/my-app.git'
                }
            }
        }
        stage("maven") {
            steps {
                sh "mvn clean package"
                sh "mv target/*.war myweb.war"
            }
        }
        stage("tomcat") {
            steps {
                script {
                    sshagent(['tomcat']) {
                        sh """
                            scp -o StrictHostKeyChecking=no /target/myweb.war root@172.31.41.28:/opt/apache-tomcat-9.0.80/webapps/
                            ssh root@172.31.41.28 '/opt/apache-tomcat-9.0.80/bin/shutdown.sh'
                            ssh root@172.31.41.28 '/opt/apache-tomcat-9.0.80/bin/startup.sh'
                        """
                    }
                }
            }
        }
    }

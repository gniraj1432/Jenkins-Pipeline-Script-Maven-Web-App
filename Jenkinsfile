pipeline {
    agent any
        environment {
            PATH = "$PATH:/opt/apache-maven-3.9.4/bin"
        }
    stages {
        stage('Get Code') {
            steps {
               git "https://github.com/gniraj1432/Jenkins-Pipeline-Script-Maven-Web-App.git"
            }
        }
         stage('Build Code') {
            steps {
               sh "mvn clean package"
            }
        }
         stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar-Server-7.8') {
                    sh "mvn sonar:sonar"
                }
            }
        }
        stage('Code Deploy') {
            steps {
                sshagent(['Tomcat-Server-Agent']) {
                    sh "scp -o StrictHostKeyChecking=no target/01-maven-web-app.war ec2-user@3.109.122.179:/home/ec2-user/apache-tomcat-9.0.78/webapps"

                }
                
            }
        }
    }
}
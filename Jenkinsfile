pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    environment {
        TOMCAT_IP = "172.31.39.78"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jagankaviad/jenkinsproject.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                scp target/jenkinsapp.war ec2-user@172.31.39.78:/opt/tomcat/webapps/
                '''
            }
        }
    }
}

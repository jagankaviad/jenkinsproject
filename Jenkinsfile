pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    environment {
        TOMCAT_IP = "172.31.39.78"
        KEY = "KEY = "/var/lib/jenkins/.ssh/id_rsa""
    }

    stages {

        stage('Check Tools') {
            steps {
                sh 'echo $PATH'
                sh 'which mvn'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                chmod 400 $KEY
                scp -o StrictHostKeyChecking=no -i $KEY target/jenkinsapp.war ec2-user@$TOMCAT_IP:/opt/tomcat/webapps/
                '''
            }
        }
    }
}

pipeline {
    agent any
    environment{
        PATH = "/opt/maven/apache-maven-3.6.3/bin:$PATH"
    }

    stages {
        stage('git') {
            steps {
                git credentialsId: 'git_cred', url: 'https://github.com/VyshakVS/ProjectJenkins.git'
            }
        }
        stage('build code') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('deploy') {
            steps {
               sshagent(['git_tomcat']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@52.66.213.79:/opt/apache-tomcat-8.5.57/webapps"
                }
            }
        }
    }
}


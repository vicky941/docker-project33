pipeline {
    agent any
    environment {
        PATH ="$PATH:/opt/apache-maven-3.9.5/bin"
    }
    stages {
        stage('getcode') {
            steps {
                git 'https://github.com/vicky941/docker-project33.git'
            }
        }
        stage('mvn package') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQubeAnalysis') {
            steps {
                withSonarQubeEnv('sonarqube-9.9.2') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}

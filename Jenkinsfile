pipeline {
    agent any
    environment {
        PATH ="$PATH:/opt/apache-maven-3.9.5/bin"
    }
    stages {
        stage('get code') {
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
        stage('Dockerbuild & docker Push & create docker container') {
            steps {
                script {
                     sh 'docker build -t venky7287/marolix:latest -f /var/lib/jenkins/workspace/jenkinspipeline/Dockerfile .'
                     
                     withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'venky7287', passwordVariable: 'dckr_pat_UtDVNl0Wpxbfg-GMV0agbcKMCJ4')]) {
                    sh '''
                        docker login -u venky7287 -p dckr_pat_UtDVNl0Wpxbfg-GMV0agbcKMCJ4
                        docker push venky7287/marolix:latest
                    '''
                    sh 'docker run -itd --name docker1263564635 -p 8060:80 venky7287/marolix:latest'
                     }
                } 
            }
        }
    }
}

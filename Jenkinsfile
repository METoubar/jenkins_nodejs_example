pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -f Dockerfile . -t mtoubar/jenkins_node:v1.0'
            }
        }
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId:"dockerhub",usernameVariable:"USERNAME",passwordVariable:"PASSWORD")]) {
                    sh 'docker login --username $USERNAME --password $PASSWORD'
                    sh 'docker push mtoubar/jenkins_node:v1.0'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 3000:3000 mtoubar/jenkins_node:v1.0'
            }
        }
    }
}
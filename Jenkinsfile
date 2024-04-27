pipeline {
    agent any

    stages {
        stage('Clone code') {
            steps {
                echo 'Clone code'
                git url: "https://github.com/Gaurav-Jain6928/django-notes-app.git", branch: "main"
            }
        }
        stage('Build image') {
            steps {
                echo 'Build image'
                sh "docker build -t my-note-app ."
            }
        }
        stage('Push image') {
            steps {
                echo 'Push image'
                withCredentials([usernamePassword(credentialsId:"dockerHub", passwordVariable: "dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage('Deployment') {
            steps {
                echo 'Deployment'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "cloning the code"
                git url: "https://github.com/Gaurav-Jain6928/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps{
                echo "bulinding the image"
                sh "docker build . -t my-note-app"
            }
        }
        stage("push to docker"){
            steps{
                echo "pushing image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHUB",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

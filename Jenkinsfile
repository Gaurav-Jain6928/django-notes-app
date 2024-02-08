pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                  echo "Cloning the code"
                  git url: "https://github.com/Gaurav-Jain6928/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                   echo "Building the image"
                   sh "docker build . -t my-note-app"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                  echo "Pushing code to docker"
                  withCredentials([usernamePassword(credentialsId:"dockerHub", passwordVariable:"dockerHubPass",usernameVariable:"dockerHubuser")]){
                  sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                  sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
         stage("Deploy"){
            steps {
                   echo "Deploying code to container"
                   sh "docker-compose down && docker-compose up -d"
           }
        }
    }
}

pipeline {
    agent any
    
    stages{
        stage("code"){
            steps{
                echo "clone the code"
                git url: "https://github.com/jajati1993/node-todo-cicd.git" , branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
            echo "Build the code"
            sh "docker build . -t node-app-demo"
            }
        }
        stage("Push to repo"){
            steps{
                echo "push to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubpass}"
                    sh "docker tag node-app-demo ${env.dockerHubUser}/node-app-demo:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-demo:latest"
                }
            }
        }
        stage("Deply"){
            steps{
               sh "docker-compose down && docker-compose up -d"
               
            }
        }
    }
}
  


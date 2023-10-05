pipeline{
    agent any
    
    stages{
        stage("Code cloned"){
            steps{
                git url: "https://github.com/ManishNegi963/node-todo-cicd.git" ,branch: "master"
            }
        }
        stage("Code build"){
            steps{
               sh "docker build . -t node-todo-app1:latest"
            }
        }
        stage("Code push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-todo-app  ${env.dockerHubUser}/node-todo-app1:latest"
                    sh "docker push ${env.dockerHubUser}/node-todo-app1:latest"
                }
            }
        }
        stage("Code deploy"){
            steps{
               sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

pipeline{
    agent {label "dev"}
    
    stages{
        stage("Code cloned"){
            steps{
                git url: "https://github.com/ManishNegi963/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Code build"){
            steps{
                sh  "docker build . -t node-app-agent"
            }
        }
        stage("Code pushed to docker"){
            steps{
               withCredentials([usernamePassword(credentialsId:"Docker-hub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                   sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                   sh "docker tag node-app-agent ${dockerHubUser}/node-app-agent"
                   sh "docker push ${dockerHubUser}/node-app-agent"
               }
            }
        }
        stage("Code deployed"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

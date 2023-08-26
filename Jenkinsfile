pipeline {
    agent { label 'dev-node' } 
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/ManishNegi963/node-todo-cicd.git',branch: 'master'
            }
        }
        stage('Build and test'){
            steps {
                sh 'docker build . -t mnmanish/node-todo-app:latest'
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'Logging into dockeHub and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push mnmanish/node-todo-app"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        } 
    }
}

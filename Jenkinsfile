pipeline {
    agent {label "dev-server"}
    stages {
        stage("clone code"){
            steps{
                git url : "https://github.com/patelajay745/node-todo-cicd.git",branch : "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-app-test"
            }
            
        }
        stage("push to docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                sh "docker tag node-app-test ${env.dockerUser}/node-app-test:latest"
                sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                sh "docker push ${env.dockerUser}/node-app-test:latest"
                }
            }
            
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}

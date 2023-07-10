pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/hamzarehmansheikh4/Django-Notes-App-Using-Jenkins.git", branch : "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t myapp ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag myapp ${env.dockerHubUser}/myapp:1.0"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/myapp:1.0"
                }
                }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}

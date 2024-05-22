
pipeline{
    agent any 
    stages{
        stage("Code"){
            steps{
                echo"code has been cloned"
                git url : "https://github.com/kajoltamiya/django-notes-app.git", branch : "main"
            }
        }
         stage("Build"){
            steps{
                echo"application has been built"
                sh "sudo docker build -t notes-app ."
            }
        }
         stage("Pushing the iamges to DockerHub"){
            steps{
                echo"images pushed to dockerHub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app ${env.dockerHubUser}/notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker login"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
         stage("Deploy"){
            steps{
                echo"deployed the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
    
}

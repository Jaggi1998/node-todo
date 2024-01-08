pipeline {
    agent any 
    stages {
        stage ("Code") {
            steps {
               git url: "https://github.com/Jaggi1998/node-todo.git" , branch: "main"
               echo "Code Clones successfully"
            }
        }
        stage ("Build and Test") {
            steps {
               sh "docker build -t node-app ."
               echo "Code build and test successfully"
            }
        }
        stage ("scan images") {
            steps {
               echo "Image scanned successfully"
            }
        }
        stage ("push") {
            steps {
                withCredentials([usernamePassword(credentialsId:"Dockerhub-credentials",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                   sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                   sh "docker push ${env.dockerHubUser}/node-app:latest"
                   echo "image push successfully"
                    
                }
            }
        }
        stage ("Deploy") {
            steps {
               sh "docker-compose down && docker-compose up -d"
               echo "code deployed succesfully"
            }
            
        }
    }
}

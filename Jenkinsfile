pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            step{
                script{
                  git branch: 'main', url: 'https://github.com/shreejejurkar/java-app-cicd.git'  
                }
            }
        }
    }
}
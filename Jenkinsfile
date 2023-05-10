@Library('my-shared-library') _

pipeline{
    agent any
    stages{
        
        stage("Git Checkout"){
            
            steps{
                
                script{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/shreejejurkar/java-app-cicd.git"
                    )  
                }
            }
        }
        stage('Unit Test Maven'){
            
            steps{
                
                script{
                    mvnTest()  
                }
            }
        }
        stage('Intigration Test Maven'){
            
            steps{
                
                script{
                    mvnIntegrationTest()  
                }
            }
        }
    }
}
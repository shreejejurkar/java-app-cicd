@Library('my-shared-library') _

pipeline{
    agent any
    parameters{
        choice(name: 'action', choices:'create\ndestroy', description:'Choose create/destroy')
    }
    
    stages{
              
        stage("Git Checkout"){

        when{expression{params.action == 'create'}}

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
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    mvnTest()  
                }
            }
        }
        
        stage('Intigration Test Maven'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    mvnIntegrationTest()  
                }
            }
        }
    }
}
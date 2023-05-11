@Library('my-shared-library') _

pipeline{
    agent any
    parameters{
        choice(name: 'action', choices:'create\ndestroy', description:'Choose create/destroy')
        string(name:'ImageName', description:'name of the docker build',defaultValue:'javaapp')
        string(name:'ImageTag', description:'tag of the docker build',defaultValue:'v1')
        string(name:'DockerHubUser', description:'name of the application',defaultValue:'shreejejurkar')
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
        stage('static code analysis: sonarqube'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    def SonarQubecredentialsId = 'sonar-api'
                    statiCodeAnalysis(SonarQubecredentialsId)  
                }
            }
        }
        stage('Quality Gate Status: Sonarqube'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    def SonarQubecredentialsId = 'sonar-api'
                    QualityGateStatus(SonarQubecredentialsId)  
                }
            }
        }
        stage('Maven Build: Maven'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    mvnBuild()
                }
            }
        }
        stage('Docker Build: Docker'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                }
            }
        }
        stage('Docker Build: Docker'){
        
        when{expression{params.action == 'create'}}

            steps{
                
                script{
                    dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                }
            }
        }
    }
}
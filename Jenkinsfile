@Library('my-shared-library') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "name of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the docker build", defaultValue: 'Pvass24')
    }

    stages{

        stage('Git Checkout'){

            when{ expression { params.action == 'create'} }

            steps {
            gitCheckout(
                branch: "main",
                url: "https://github.com/pvass24/Jenkins-CI-CD-Pipeline.git"
            )
            }
        }

        

        stage('Unit Test Maven'){

        when{ expression { params.action == 'create'} }

            steps {
                script{
                    mvnTest()
                }
            }
        }

        stage('Maven Integration Test'){

        when{ expression { params.action == 'create'} }    
            steps {
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis: SonarQube'){

        when{ expression { params.action == 'create'} }    
            steps {
                script{
                    def credentialsId = 'sonarqube-api'
                    statiCodeAnalysis(credentialsId)
                }
            }
        }

        stage('Quality Gate Status Check:SonarQube'){

        when{ expression { params.action == 'create'} }    
            steps {
                script{
                    def credentialsId = 'sonarqube-api'
                    QualityGateStatus(credentialsId)
                }
            }
        }

        stage('Maven Build'){

        when{ expression { params.action == 'create'} }    
            steps {
                script{

                    mvnBuild()

                }
            }
        }

        stage('Docker Image Build'){

        when{ expression { params.action == 'create'} }    
            steps {
                script{

                    dockerBuild("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")

                }
            }
        }

        
    }

   
}
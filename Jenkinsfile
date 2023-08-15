@Library('my-shared-library') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
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
                    def SonarQubecredentialsId = 'Sonarqube-api'
                    statiCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
    }

   
}
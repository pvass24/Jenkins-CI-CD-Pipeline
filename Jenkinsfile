@Library('my-shared-library') _

pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps {
            gitCheckout{
                branch: "main",
                url: "https://github.com/pvass24/Jenkins-CI-CD-Pipeline.git"
            }
            }
        }

        stage('Unit Test Maven'){
            
            steps {
                script{
                    mvnTest()
                }
            }
        }
    }

   
}
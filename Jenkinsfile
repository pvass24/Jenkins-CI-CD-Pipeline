@Library('my-shared-library') _

pipeline{

    agent any

    stages{

        stage('Git Checkout'){
            steps {
                script{

                    git branch: 'main', url: 'https://github.com/pvass24/Jenkins-CI-CD-Pipeline.git'


                }
            }
        }
    }

   
}
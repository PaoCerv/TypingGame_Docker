pipeline {
    agent any 
    stages {

        stage('Checkout code') {
            steps {
            checkout scm
            }
    }

        stage('Connection to AWS') { 
            steps {
                script{
                    sh '''
                        aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin 435053451664.dkr.ecr.us-west-1.amazonaws.com
                        
                   '''
                } 
            }
        }
        stage('Build') { 
            steps {
                script{
                    
                    sh '''
                        
                       docker build -t typing_game . 
                       docker tag typing_game:latest 435053451664.dkr.ecr.us-west-1.amazonaws.com/mentorship_repository:latest
                       docker push 435053451664.dkr.ecr.us-west-1.amazonaws.com/mentorship_repository:latest
                       
                   '''
                } 
            }
        }

        stage('Create repository') { 
            steps {
                script{
                    sh '''
                        
                       aws ecs create-cluster --cluster-name MyClusterPao
                   '''
                } 
            }
        }






        // stage('Test') { 
        //     steps {
        //         // 
        //     }
        // }
        // stage('Deploy') { 
        //     steps {
        //         // 
        //     }
        // }
    }
}
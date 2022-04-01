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
                        aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 435053451664.dkr.ecr.us-east-2.amazonaws.com
                        
                   '''
                } 
            }
        }
        stage('Build') { 
            steps {
                script{
                    #docker rmi typing_game
                    sh '''
                        
                       docker build -t typing_game . 
                       docker tag typing_game:latest 435053451664.dkr.ecr.us-east-2.amazonaws.com/pao_repository:latest
                       docker push 435053451664.dkr.ecr.us-east-2.amazonaws.com/pao_repository:latest
                       
                   '''
                } 
            }
        }

        stage('Create cluster') { 
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
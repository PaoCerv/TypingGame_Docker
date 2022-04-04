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

        stage('Create cluster') { 
            steps {
                script{
                    sh '''
                        
                       aws ecs create-cluster --cluster-name MyCluster
                       
                       
                   '''
                } 
            }
        }

        stage('Test ecs pluggin TASK DEFINITION') {
            steps {
                ecs {
                    inheritFrom 'label-of-my-preconfigured-template'
                    cpu 256
                    memory 512
                    image '435053451664.dkr.ecr.us-west-1.amazonaws.com/mentorship_repository:latest'
                    logDriver 'fluentd'
                    logDriverOptions([[name: 'foo', value:'bar'], [name: 'bar', value: 'foo']])
                    portMappings([[containerPort: 8080, hostPort: 8080, protocol: 'tcp'], [containerPort: 443, hostPort: 443, protocol: 'tcp']])
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
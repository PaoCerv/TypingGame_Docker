// import groovy.json.JsonSlurperClassic
// def jsonParse(def json) {

//     new groovy.json.JsonSlurperClassic().parseText(json)

// }

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

                        aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/d9z3m8e7
                   '''
                } 
            }
        }
        stage('Build') { 
            steps {
                script{
                    
                    sh '''
                       
                       docker build -t typing_game . 
                       docker tag typing_game:latest public.ecr.aws/d9z3m8e7/mentorship_repository2:latest
                       docker push public.ecr.aws/d9z3m8e7/mentorship_repository2:latest
                       
                   '''
                } 
            }
        }

        stage('Create cluster') { 
            steps {
                script{
                    sh '''
                        
                        aws ecs create-cluster --cluster-name MyCluster
                        aws ecs register-task-definition --cli-input-json file://taskDefinition.json
                        aws ecs create-service --cluster MyCluster --service-name fargate-service --task-definition sample-fargate:1 --desired-count 1 --launch-type "FARGATE" --network-configuration "awsvpcConfiguration={subnets=[ subnet-00d2456e10f182a79],securityGroups=[sg-00d3ae2d9784e294c],assignPublicIp=ENABLED}"

                       
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

                                //aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin 435053451664.dkr.ecr.us-west-1.amazonaws.com
    }
}
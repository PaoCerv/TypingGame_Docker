pipeline {
    agent any 
    stages {

        stage('Checkout code') {
            steps {
            checkout scm
            }
    }

        stage('Build') { 
            steps {
                script{
                    
                        dockerImage = docker.build imagename
                   
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
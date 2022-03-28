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
                    sh """
                        docker build .
                    """
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
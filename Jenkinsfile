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
                'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
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
pipeline {

  agent any

  environment {

    appName = "variable"

  }

  stages {



 stage("paso 1"){

     

      steps {

          script {      

           sh "echo 'hola mundo' 'ls -la'"
           

        }

      }

    }

  }

  post {

      always {          

          deleteDir()

           sh "echo 'fase always'"

      }

      success {

            sh "echo 'fase success'"

        }



      failure {

            sh "echo 'fase failure'"

      }

     

  }

}  
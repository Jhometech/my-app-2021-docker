pipeline{
  agent any

  stages{
    stage('Maven Build'){
      steps{
        sh "mvn clean package"
      }
    }

    stage('Docker Build Image'){
      steps{
        sh "docker build -t kammana/2021myapp:v1 . "
      }
    }
    
    stage('push to docker hub'){
      steps{
        echo "deploy to dev environment"
      }
    }

    stage('dev-deploy'){

      steps{
        echo "deploy to uat environment"
      }
    }
  }
}

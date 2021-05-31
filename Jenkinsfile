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
        withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
          sh "docker login -u kammana -p ${dockerPwd}"
          sh "docker push kammana/2021myapp:v1"
        }
        
      }
    }

    stage('dev-deploy'){

      steps{
        echo "deploy to uat environment"
      }
    }
  }
}

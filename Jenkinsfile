pipeline{
  agent any

  tools{
    maven 'maven3'
  }
  stages{
    stage('Maven Build'){
      steps{
        sh "mvn clean package"
      }
    }

    stage('Upload To Nexus'){
      steps{
        nexusArtifactUploader artifacts: 
          [[artifactId: 'myweb', classifier: '', file: 'target/myweb-0.0.1-SNAPSHOT.war', type: 'war']], 
          credentialsId: 'nexus3', 
          groupId: 'in.javahome', 
          nexusUrl: '172.31.4.89:8081', 
          nexusVersion: 'nexus3', protocol: 'http', 
          repository: 'javahome-snapshot', 
          version: '0.0.1-SNAPSHOT'
      }
    }
    

    
    stage('dev-deploy'){
      when {
        branch "dev"
      }
      steps{
        echo "deploy to dev environment"
      }
    }
  }
}

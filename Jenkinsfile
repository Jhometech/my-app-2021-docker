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
        script{
          def pom = readMavenPom file: 'pom.xml'
          nexusArtifactUploader artifacts: 
          [[artifactId: 'myweb', classifier: '', file: "target/myweb-${pom.version}.war", type: 'war']], 
          credentialsId: 'nexus3', 
          groupId: 'in.javahome', 
          nexusUrl: '172.31.4.89:8081', 
          nexusVersion: 'nexus3', protocol: 'http', 
          repository: 'javahome-snapshot', 
          version: pom.version
        }
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

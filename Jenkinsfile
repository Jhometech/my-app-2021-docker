pipeline{
  agent any

  stages{
    stage('Maven Build'){
      when {
        branch "develop"
      }
      steps{
        sh "mvn clean package"
      }
    }

    stage('Upload To Nexus'){
      when {
        branch "develop"
      }
      steps{
        script{
          def pom = readMavenPom file: 'pom.xml'
          def repository = pom.version.endsWith("SNAPSHOT") ? 'javahome-snapshot' : 'javahome-release'
          nexusArtifactUploader artifacts: 
          [[artifactId: 'myweb', classifier: '', file: "target/myweb-${pom.version}.war", type: 'war']], 
          credentialsId: 'nexus3', 
          groupId: 'in.javahome', 
          nexusUrl: '172.31.4.89:8081', 
          nexusVersion: 'nexus3', protocol: 'http', 
          repository: repository, 
          version: pom.version
        }
      }
    }
    
    stage('dev-deploy'){
      when {
        branch "develop"
      }
      steps{
        echo "deploy to dev environment"
      }
    }

    stage('uat-deploy'){
      when {
        branch "uat"
      }
      steps{
        sh "curl -u admin:admin -X GET 'http://65.0.19.206:8081/service/rest/v1/repositories'"
        // How do you get latest artifact from nexus?
        echo "deploy to uat environment"
      }
    }

    stage('prd-deploy'){
      when {
        branch "master"
      }
      steps{
        // How do you get latest artifact from nexus?
        echo "deploy to prod environment"
      }
    }
  }
}

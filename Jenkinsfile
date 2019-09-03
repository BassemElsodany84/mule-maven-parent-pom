pipeline {
  agent any
  tools {
    maven 'apache-maven-3.6.1'
  }
  stages {
    
    stage('Unit Test') { 
      steps {
      echo '********************************** Unit Test Stage **********************************'
        sh 'mvn clean install -DskipTests'
      }
    }
    
    stage('Deploy Standalone') { 
      steps {
       echo '********************************** Deploy Standalone Version. **********************************' 
        sh 'mvn package deploy -P standalone -DmuleDeploy -X'
      }
    }
    

    
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
      echo '********************************** Deploy CloudHub Version **********************************'
        sh 'mvn package deploy -P cloudhub -DmuleDeploy -Danypoint.username=${ANYPOINT_CREDENTIALS_USR}  -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW} -X' 
      }
    }
  }
}
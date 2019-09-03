pipeline {
  agent any
  tools {
    maven 'apache-maven-3.6.1'
  }
  stages {
    
    # stage('Unit Test') { 
     #  steps {
      #   sh 'mvn clean test -X'
      # }
   #  }
    
    stage('Deploy Standalone') { 
      steps {\
       echo '======================== Deploy Standalone Version. ========================' 
        sh 'mvn --projects ricston-hello-world --also-make clean deploy -P standalone -DmuleDeploy -X'
      }
    }
    

    
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
      echo '======================== Deploy CloudHub Version. ========================'
        sh 'mvn clean deploy -P cloudhub -DmuleDeploy -Danypoint.username=${ANYPOINT_CREDENTIALS_USR}  -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW} -X' 
      }
    }
  }
}
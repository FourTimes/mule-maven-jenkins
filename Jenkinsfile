pipeline {
  agent any
  stages {
    stage('Unit Test') {
      steps {
        sh ''' export PATH=/usr/local/bin/apache-maven/bin:$PATH
               mvn clean test
               '''
      }
    }
    stage('Deploy ARM') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh '''
           export PATH=/usr/local/bin/apache-maven/bin:$PATH 
           mvn deploy -P arm -Darm.target.name=local-3.9.0-ee -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}
           '''
      }
    }
    stage('Deploy CloudHub') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh '''
           export PATH=/usr/local/bin/apache-maven/bin:$PATH'
           mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}
           '''
      }
    }
  }
}

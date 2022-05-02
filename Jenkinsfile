pipeline {
  
  agent any
  
  tools {
    maven 'Maven'
    
    parameters {
      choice(name: 'VERSION', choices: ['1.1.0', '1.2.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '') 
    
  
  environment {
    SERVER_CREDENTIALS = credentials ('da0b8891-c80c-4073-91b9-d91fb46849d2')
  }  
  
  stages {
    
    stage("build") {
      
      steps {
        echo 'building the application...'
        echo 'changed now'
      }
    }
    
    stage("test") {
      when {
        expression {
          params.executeTests
        }
      }
      steps {
        echo 'testing the application....'
      }
    }
    stage("deploy"){
      
      steps {
        echo 'deploying the application....'
        echo "deploying with ${SERVER_CREDENTIALS}"
        sh "${SERVER_CREDENTIALS}"
        withCredentials([
          usernamePassword( credentials: 'da0b8891-c80c-4073-91b9-d91fb46849d2', usernameVariable: USER, passwordVariable: PWD)
          )]
                        { 
                          sh "some script ${USER} ${PWD} "  
                        }
      }
    }
  }
}

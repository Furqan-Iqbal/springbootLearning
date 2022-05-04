pipeline {
  environment {
    Rancher_Jekens_key = "-Duser.home=/home/jenkins"
  }
  agent any {
    dockerfile {
      lable "docker"
      args "-v /tmp/maven:/home/jenkins/.m2 -e MAVEN_CONFIG=/home/jenkins/.m2"
    }
  }
  stages {
    stage('Build') {
      steps {
        sh "ssh -V"
        sh "mvn -version"
        sh "mvn clean install"
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}

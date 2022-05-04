pipeline {
  agent any
  environment {
    Rancher_Jekens_key = credentials('rancher-jekens-key')
  }
    
    stage('Build') {
      steps {
        sh 'docker build -t registry.hiqs.de/java-web-app:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $registry.hiqs.de | docker login --username=furqan.iqbal --password=Haiderali@313 registry.hiqs.de'
      }
    }
    stage('Push to Heroku registry') {
      steps {
        sh '''
          docker tag registry.hiqs.de/java-web-app:latest registry.hiqs.de/$APP_NAME/web
          docker push registry.hiqs.de/$APP_NAME/web
        '''
      }
    }
    stage('Release the image') {
      steps {
        sh '''
          heroku container:release web --app=$APP_NAME
        '''
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

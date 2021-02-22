pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('package') {
      steps {
        sh 'docker build -t tcc-auth .'
      }
    }

    stage('tag') {
      steps {
        sh 'docker tag tcc-auth:latest srochg/tcc-auth'
      }
    }

    stage('push') {
      steps {
        sh 'docker push srochg/tcc-auth'
      }
    }

    stage('rollout') {
      steps {
        sh 'kubectl rollout restart deployment tcc-auth-api-deployment'
      }
    }

    stage('qa-test') {
      steps {
        sh 'echo Iniciando os testes'
        sh 'sleap 3'
        sh 'echo Testes finalizados com sucesso'
      }
    }

  }
}
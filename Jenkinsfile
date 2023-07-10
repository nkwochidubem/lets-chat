pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/nkwochidubem/lets-chat', branch: 'main')
      }
    }

    stage('log') {
      steps {
        sh 'ls -al'
      }
    }

    stage('Build Frontend') {
      steps {
        sh 'docker build -f frontend/Dockerfile -t nkwochidubem/lets-chat-frontend:latest .'
      }
    }

    stage('Build backend') {
      steps {
        sh 'docker build -f server/Dockerfile -t nkwochidubem/lets-chat-backend:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_USER = 'nkwochidubem'
        DOCKERHUB_PASSWORD = 'icui4cu5517'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push Frontend') {
      steps {
        sh 'docker push nkwochidubem/lets-chat-frontend:latest'
      }
    }

    stage('Push Backend') {
      steps {
        sh 'docker push nkwochidubem/lets-chat-backend:latest'
      }
    }

    stage('Deploy') {
      environment {
        DOCKERHUB_USER = 'nkwochidubem'
        DOCKERHUB_PASSWORD = 'icui4cu5517'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
        sh 'docker compose --context client1 up -d --no-color --wait'
      }
    }

  }
}

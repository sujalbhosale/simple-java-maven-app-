pipeline {
  agent any

  tools {
    jdk 'jdk21'
    maven 'maven3'
    docker 'docker'
  }

  stages {

    stage('Clone Code') {
      steps {
        git 'https://github.com/vaishnavi08072000/simple-java-maven-app.git'
      }
    }

    stage('Build Application') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t demo-app .'
      }
    }

    stage('Deploy Container') {
      steps {
        sh '''
        docker stop demo-container || true
        docker rm demo-container || true
        docker run -d -p 8081:8081 --name demo-container demo-app
        '''
      }
    }
  }
}

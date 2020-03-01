pipeline {
    agent any
    stages {
        stage('Git Checkout') {
        steps {
            echo 'Checkout'
            git 'https://github.com/Bondalive/deploytest.git'
        }
        }
          stage('SonarQube analysis') {
        steps {
     echo 'Sonar analysis'
     tool name: 'sonarscanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
          }
        }
        stage('clean') { 
            steps {
                echo 'cleaning..'
                bat 'mvn clean'
                }
        }
    stage('Package') {
    steps {
    echo 'Testing..'
    bat 'mvn package'
    }
    }
    stage('Deploy') {
    steps {
    echo 'Deploying....'
    deploy adapters: [tomcat8(credentialsId: 'tomcat_credentials', path: '', url: 'http://localhost:9999/')], contextPath: null, war: '**/*.war'
    }
    }
    stage('Email') {
    steps {
    echo 'email sent..'
    emailext body: 'Check the code', subject: 'Hi', to: 'vish.sira@gmail.com'
    }
    }
    }
}

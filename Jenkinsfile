pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    environment {
        SONARQUBE_ENV = 'SonarQube'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Iriya17/devops-ci-pipeline.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                      mvn sonar:sonar \
                      -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed'
        }
    }
}

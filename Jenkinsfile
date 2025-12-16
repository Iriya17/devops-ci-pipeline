pipeline {
    agent any

    tools {
        maven 'Maven'
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
            environment {
                SONAR_TOKEN = credentials('sonar-token')
            }
            steps {
                sh '''
                  mvn sonar:sonar \
                  -Dsonar.login=$SONAR_TOKEN \
                  -Dsonar.host.url=http://host.docker.internal:9000
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed'
        }
    }
}

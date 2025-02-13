pipeline {
    agent {
        docker {
            image 'node:10-alpine'
        }
    }

    environment {
        SONARQUBE_URL = 'http://sonarqube:9000'  // Ensure this matches your SonarQube server URL
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Set the SonarQube scanner tool
                    def scannerHome = tool name: 'sonarqube', type: 'SonarQubeScanner'
                    withSonarQubeEnv('sonarqube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=${SONARQUBE_URL}"
                    }
                }
            }
        }
    }
}
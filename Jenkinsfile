pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true 
        }
    }

    stages {
        stage('SCM'){
            steps {
                checkout scm
            }
        }
        stage('install dependencies'){
            steps {
                sh 'npm install'
            }
        }
        stage('build'){
            steps {
                sh 'npm run build'
            }
        }
        
        stage('SonarQube Analysis') {
    agent any // Runs outside the Docker container
    steps {
        script {
            def scannerHome = tool 'sonarqube' // Use the name you configured in the global tools section
            withSonarQubeEnv() { // Set up the environment for SonarQube
                sh "${scannerHome}/bin/sonar-scanner" // Run the SonarQube scanner
            }
        }
    }
}
}
}
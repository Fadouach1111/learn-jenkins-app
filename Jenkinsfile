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
        
        stage('SonarQube Analysis'){
            agent any
            steps {
                def scannerHome = tool 'sonarqube';
                withSonarQubeEnv() {
                    sh "${scannerHome}/bin/sonar-scanner"
            }
        }
    }
}
}
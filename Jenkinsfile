pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true 
        }
    }

    stages {
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
        stage('SCM'){
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis'){
            steps {
                def scannerHome = tool 'sonarqube';
                withSonarQubeEnv() {
                    sh "${scannerHome}/bin/sonar-scanner"
            }
        }
    }
}
}
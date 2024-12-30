pipeline {
    agent any

    tools {
        nodejs 'sonarnode'  
    }
    
    environment {
        NODEJS_HOME = 'C:\\Program Files\\nodejs'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install and Build') {
            steps {
                bat '''npm install
                npm run lint'''  
            }
        }

        
        stage('SonarCodeAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-token')  
            }
            steps {
                bat '''
                sonar-scanner ^
                -Dsonar.projectKey=Mern_Backend ^
                -Dsonar.sources=. ^
                -Dsonar.host.url=http://localhost:9000 ^
                -Dsonar.token=sqp_f4f0cbc73d62a791503647c7a8a6d0c7a80db215 ^
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline SUCCESSFULLY Build"
        }
        failure {
            echo " Pipeline failed"
        }
    }
}

pipeline {
    agent any
            
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anjalikota10/tetris-game.git'
            }
        }

      stage('Trivy FS Scan') {
            steps {
                sh 'trivy fs --format table -o fs-report.html .'
            }
        }

      stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {  
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=TaskMaster \
                    -Dsonar.projectName=TaskMaster -Dsonar.java.binaries=target '''
                    
                 }    
            }
        }

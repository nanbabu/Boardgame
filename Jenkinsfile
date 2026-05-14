pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
    SCANNER_HOME = tool 'sonar-scanner'
}
    
    stages {   
        stage('Compile') {
            steps {
            git branch: 'main', url: 'https://github.com/nanbabu/Boardgame.git'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Sonar') {
            steps {
                withSonarQubeEnv('sonar') {
                          sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Python-project \
                          -Dsonar.projectName=Python-project \
                          -Dsonar.sources=. \
                          -Dsonar.python.coverage.reportPaths=coverage.xml'''
                }
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
    }
}

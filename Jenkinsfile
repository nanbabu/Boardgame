pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    stages {   
        stage('Compile') {
            steps {
            sh 'mvn compile'
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

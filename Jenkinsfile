pipeline {
    agent any

    stages{
        stage('fetch code') {
          steps{
             git credentialsId: 'github credentials', url: 'https://github.com/yashika-siva/realtimeproject.git'
          }  
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }

        }
         stage('Code Ananlysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }

        }
        
    }
}


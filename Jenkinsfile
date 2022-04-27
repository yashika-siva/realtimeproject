pipeline {
    agent any

    stages{
        stage('fetch code') {
          steps{
             git credentialsId: '5d71a719-f75f-41ca-9da3-8a558a356e29', url: 'git@github.com:yashika-siva/realtimeproject.git'
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


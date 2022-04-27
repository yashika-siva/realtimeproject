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
        stage('nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/test-repo-v1.war', type: 'war']], credentialsId: 'c217ec9d-cd56-47e9-aa73-ebc19fa47339', groupId: 'com.visualpathit', nexusUrl: '18.220.149.146:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'test-repo', version: 'v1'
            }

        }
    }
}


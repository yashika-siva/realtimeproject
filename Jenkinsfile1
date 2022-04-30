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
        stage('deploy to container'){
            steps {
                sh "curl -v -u sivaparvathi:Yashika@09 -T /var/lib/jenkins/workspace/job1/target/vprofile-v1.war 'http://18.222.225.193:4000/manager/text/deploy?path=/maven'"
            }

        }
        
    }
}


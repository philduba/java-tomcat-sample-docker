pipeline {
    agent any
    tools {
        maven 'LocalMaven'
    }
    stages{
        stage('Build Application') {
            steps{
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success{
                    echo "Now Archiving the Artificats ..."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Create Tomcat Docker Image'){
            steps{
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
    }
}
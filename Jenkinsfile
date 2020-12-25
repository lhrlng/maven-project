pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success{
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }
        stage('Bla2'){
            steps {
                echo 'Code Bla2.'
            }
        }
    }
}